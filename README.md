# create-svelte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

To run this project locally please type in the command

```bash
npm install

npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```


## Todo
1. Add filters
I didn't have time to work on filters but could get something up and running in an hour or so!

2. Aria labels and focus
This site isn't very accessible or responsive. I've implemented only the bare minumum

3. Type safety
Since I'm completely new to svelte i didn't want to spend time wrapping my head around how it would work with TypeScript although now I understand that it's pretty standard. Future work would entail re-writing most of the app in TS.

4. Tests
For an app this small I didn't want to spend time writing tests, though it seems like the built in vitest is pretty awesome in that regard

5. Deploy
Could have hosted it on vercel or something.
