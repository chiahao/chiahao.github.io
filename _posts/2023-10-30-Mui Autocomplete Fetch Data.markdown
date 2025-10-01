---
layout: post
title: "Mui Autocomplete Fetch Data"
date: 2023-10-29 18:13:00
category: mui
tags: [mui]
---

```javascript
<Autocomplete
	multiple={false}
	options={natOption}
	id="natcod_descr"
	name="natcod_descr"
	onChange={handleNatOptionChange}
	value={data.natcod_descr ? {"DESCR": data.natcod_descr} : null}
	getOptionLabel={(option) => `${option.DESCR}`}
	renderOption={(props, option) => (
		<Box {...props}>
			{option.DESCR}
		</Box>
	)}
	onInputChange={onNatInputChange}
	renderInput={(params) => (
		<TextField
			{...params}
			label="國籍一"
			variant="outlined"
		/>)}
	isOptionEqualToValue={(option, value) => option.DESCR === value.DESCR}
	filterOptions={(x) => x}
/>
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


