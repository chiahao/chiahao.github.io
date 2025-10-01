---
layout: post
title: "SpringBoot Custom Login And Unit Test"
date: 2025-08-21 11:08:00
category: program
tags: [springboot, junit5]
---

```java
@Configuration
@EnableMethodSecurity
public class WebSecurityConfig {

	@Bean
	public InMemoryUserDetailsManager userDetailsService(PasswordEncoder passwordEncoder) {
		UserDetails user = User.withUsername("user")
				.password(passwordEncoder.encode("password"))
				.roles("USER")
				.build();

		UserDetails admin = User.withUsername("admin")
				.password(passwordEncoder.encode("admin"))
				.roles("USER", "ADMIN")
				.build();

		return new InMemoryUserDetailsManager(user, admin);
	}

	@Bean
	public SecurityFilterChain filterChain(@NotNull HttpSecurity http) throws Exception {
		return http.authorizeHttpRequests(request -> request.anyRequest()
						.authenticated())
				.httpBasic(Customizer.withDefaults())
				.build();
	}

	@Bean
	public PasswordEncoder passwordEncoder() {
		return PasswordEncoderFactories.createDelegatingPasswordEncoder();
	}
}
```


```java  
@ExtendWith(SpringExtension.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@Import(WebSecurityConfigTest.TestOnlyController.class)
public class WebSecurityConfigTest {

	private TestRestTemplate restTemplate;
	private URL base;

	@LocalServerPort
	int port;

	@BeforeEach
	public void setUp() throws MalformedURLException {
		restTemplate = new TestRestTemplate("user", "password");
		base = new URL("http://localhost:" + port);
	}

	@Test
	public void whenLoggedUserRequestsHomePage_ThenSuccess() throws IllegalStateException {
		ResponseEntity<String> response = restTemplate.getForEntity(base.toString(), String.class);

		assertEquals(HttpStatus.OK, response.getStatusCode());
		assertNotNull(response.getBody());
		String body = response.getBody();
		assertTrue(response.getBody().contains("Entry"));
	}

	@Test
	public void whenUserWithWrongCredentials_thenUnauthorizedPage() {
		restTemplate = new TestRestTemplate("user", "wrongpassword");
		ResponseEntity<String> response =
				restTemplate.getForEntity(base.toString(), String.class);

		assertEquals(HttpStatus.UNAUTHORIZED, response.getStatusCode());
		assertNull(response.getBody());
	}

	/**
	 * Custom Entry Point
	 */
	@RestController
	static class TestOnlyController {
		@GetMapping("/")
		public String home() {
			return "Entry";
		}
	}
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

