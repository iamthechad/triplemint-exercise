# Exercise App

This is a simple rendering of the Triplemint search page, with pretty minimal functionality.

Instead of going for a full-featured implementation, I went for a simpler approach that hopefully shows some of my frontend knowledge, along with the ability to grasp the basics of Svelte.

## Functionality

This app uses a JSON file of data taken from the Triplemint site. This was an easier solution for me than creating my own backend or trying to access the existing Triplemint API.

* Listings are shown in a grid format in a similar manner to the Triplemint site. Only the primary photo for each property is shown, and there is no ability to scroll through photos or do anything upon clicking the property.
* Photos can be toggle between the main photo and the floor plan. If there is no floor plan, the default photo will be used.
* There is a very simple toggle to include/exclude co-op properties.

## Decisions

I used the TypeScript template, and added support for SCSS.

I created several components to show that I understand some of the Svelte basics, including:
* Iteration over data
* Props
* Reactive values/statements
* Component events
* slots

I did not use any kind of state management since this exercise is fairly small.

I know there are several areas that are not as good as they could be, like a preponderance of `div`s and some data handling in weird places.  

# Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.


# Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).
