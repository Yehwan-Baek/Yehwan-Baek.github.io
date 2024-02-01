---
layout: post
title: "2023-04-01-CORS Error while building phase1 project"
categories: [Projects in Academy Xi]
---

Hi, I'm Yehwan. This post will be about CORS Error.

For my phase1 project, building Pokemon dictionary using the Poke API that is public API, I wanted to add other features besides to display data about Pokemon. So, I thought to add comment box and comments to be displayed after submit some comment. To do that, I need to create mock server on my local, post and get the comment data from my local db.json file. And to display comment and data of searched Pokemon, I needed to bring the value of Pokemon name from API to my local server to set the name of Pokemon for searching to be same as the name of Pokemon for commenting.

First, I created json file for data of comment, built a code to display the comment box when click event occurs on pokemon searching form. And I put code to post data to my local in fetch Poke API code because I also wanted to post name and id number of searched Pokemon.

That was posted successfully as value of pokemon name and id number that I brought from Poke API.

Then, finally, I can get comment data from local server when Pokemon is searched. To do that, I also built this fetch code inside code that fetch Poke API. However, The entire code didn't work returning this error message.

This is error message --



Access to fetch at 'https://pokeapi.co/api/v2/pokemon//' from origin 'null' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.

index.js:27          GET https://pokeapi.co/api/v2/pokemon// net::ERR_FAILED 301
searchPokemon @ index.js:27
(anonymous) @ index.js:11

index.js:163 TypeError: Failed to fetch
    at searchPokemon (index.js:27:5)
    at HTMLFormElement.<anonymous> (index.js:11:9)



I saw that for the first time. I searched for CORS. It stands for Cross-Origin Resource Sharing. It is a security feature implemented in web browsers that prevents a web page from making requests to a different domain than the one that served the web page. This is done to prevent unauthorized access to resources on a different domain.

To solve this error, I need to add headers to allow CORS request. But unluckily, It didn't work. -I still don't get why this solution didn't work.-

So I thought to create new js file for getting data from local server. I built the code that get data from local server when event of Pokemon searching Form occurs. That means searching form has a event listener function on each js files, One for the Poke API and the other for my local server.

That way, the CORS error was solved well.

In this time, I understood that I need to authorise access to public API to use other domain together.