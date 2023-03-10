# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
  I clicked the Add a Toy button on the browser app and checked the Console and Network tabs to see what error was being recieved. It was a 500 Internal Server error and checking the Network tab showed very clearly there was a NameError in the controller so I corrected the spelling in the create method and now the toy form is successful

- Update the number of likes for a toy

  - How I debugged:
  After attempting to update the likes for a toy there was an Unexpected End of JSON Input error, however the error on the browser was pointing to a fetch request on the react side, and this lab says not to modify the react side so I looked first to the controller where I quickly recognized the update method was missing the render portion, a simple fix to successfully update a toy's likes

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
Upon clicking the Donate to Goodwill button for delete functionality I checked the console to find a 404 not found error, I then checked the network tab for further details and there was a routing error, no route matching to the destroy method. I checked the routes tab in the code and added :destroy to the resources, successfully allowing a toy to be donated and deleted from the database