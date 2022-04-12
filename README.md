# Cocktail API https://www.thecocktaildb.com/api.php

### Explain what the API you are writing about does.
Cocktail API is a free API with thousands of cocktails where you can search for recipes, images of specific cocktails, ingredients, filter by alcoholic, non alcoholic, etc. 

### Show code example(s) of how you would use this API in PHP. Please put your code examples in fenced code blocks.
```
Route::get('/cocktails', function (Request $request) {
  $term = $request->query('term');

  $cacheKey = "cocktails-api-$term";

  $response = Cache::remember($cacheKey, 60, function () use ($term) {
    return Http::get("https://www.thecocktaildb.com/api/json/v1/1/search.php?s=$term")->object();
  });
  return view('api.cocktails', [
    'response' => $response,
  ]);
});
```

### If API keys or tokens are needed to use the API you are writing about, explain how to retrieve those. Please include links and screenshots.
You can use the test API key "1" during development of your app or for educational use. However you must sign up to Patreon (https://www.patreon.com/thedatadb) if you want a production API key if releasing publicly on an appstore.

### Include a screenshot of what the JSON response looks like.
<img width="1222" alt="Screen Shot 2022-04-11 at 5 19 23 PM" src="https://user-images.githubusercontent.com/54862910/162853762-0bb321d5-dee5-407d-aa28-b3f3103ee1df.png">
