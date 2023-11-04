# Django Tourist Attraction
You’ll be creating an application that allows for users to see a list of tourist attractions in each state. Users can also specify the state that they want to see more detailed attractions with as well. You’ll be creating the templates for this website, meaning that you’ll be creating everything the users see using Django!

## Instructions
### Creating a Base Template
1. Before you start writing any code, take a look at the overall structure of the application. We’ve provided some code for you already to allow you to focus just on template creation!
Things to consider and explore:
* What’s the project name? app name?
* What functions are provided in views.py?
* What paths are in urls.py?

2. Now that you’ve got a general sense of the app, let’s start by creating a base template. Right now we are getting a TemplateDoesNotExist error when we try to load our application. This is Django telling us that it’s not finding the template we’re telling it to render in the location we told it to look. To fix this, all we have to do is add in the template.
Create **base.html** in _tourist_attractions/templates/tourist_attractions_.

3. Remember that **base.html** should contain some common elements, so add some structure.
Inside of **base.html**, add
* The doctype declaration
* The <head> element
* The <body> element.

4. One common feature in all apps is to allow users to be able to navigate back to the home page.
Inside the `<body>` add a link (`<a>`) that users can click on to send them to the `"home"` path. The text inside the link should read `Take me home`.

5. Since you also want your **base.html** to be able to display page-specific content, you’ll need to add some blocks!
* Inside the `<head>` element, add a block called `head`. This block will be used for loading assets.
* In the `<body>` element, under the `<a>` element, add another block called `content`. This block will be used to display page-specific content.

### Creating the Home Page
6. Now that we have our base template created, we can start making the homepage for the application. This will be the home of every state and every attraction.
Create a new HTML page called **home.html** in the same location as **base.html**.
* Have it extend off of **base.html**
* Add a head block
* Add a content block

After implementing **home.html**, the error in the browser should be gone and you should see your link appear!

7. Currently, our page looks a little bland, to change this we need to add some CSS files. This can be done by loading in the static files. Then, load in the static file _'tourist_attractions/style.css'_.
You’ll know this is done correctly when the background color changes to a light blue.

8. We want to welcome our users to the application and tell them what they’ll be looking at. To do this, inside of the `content` block, add a `<h1>` that says something like `This is a list of attractions in America!`.

9. Now we want to show the users each attraction and what state that attraction is in. The best way to do this would be to build a table.
Under the `<h1>` add:
* A `<table>` element
* Inside the table, a table row (`<tr>`) element
* Nested in the row, individual table headings (`<th>`) for _Attraction_, _State_, and _State details_.

By now you should have a table header on the webpage with three columns being _Attraction_, _State_, and _State details_.

10. Now that we have the table mostly built, we need to go through every attraction and display it.
To get started with the process:
* Inside the `<table>` and after the first row, add a `for` loop using DTL.
* Have it loop through each `item` in `attractions`.
* Sort `attractions` based on the `state` using the filter `dictsort`.
* Make sure to include the `endfor`.

11. Now that we have the loop set up, we want to show everything about that attraction.
Inside of the `for` loop, we need to add some more HTML and DTL to display everything about the attraction. Let’s add these elements:
* A table row (`<tr>`).
* Inside of the table row, add a table detail element (`<td>`)
* This `<td>` element should display item.attraction_name.

We’ll only see the first column displayed. But we’ll continue to work on this table!

12. We still need to fill in two other columns.
Add another `<td>` element that will render `item.state`.

13. For the third column, “State details”, we’ll add a link to a separate page that lists attractions only for a specific state using the urlpattern named `details` that is pre-defined in **urls.py**.
In the table we created in **home.html**, create another `<td>` element containing a link element, `<a>`, which displays the text “State details”. The `href` attribute will use the _`url`_ built-in tag, with `'details'` as the pattern name. We can provide the state name as an argument, using the _`slugify`_ filter to remove any spacing and capitalization.

### Creating the details page
14. Now that we have every state listed out and their attractions, we can start going into details for each state in case a user wants to look at attractions for specific states.
Create a template called **details.html**. Extend the template from **base.html** and load in the CSS sheet like before.

15. Inside of the content block, add an `<h1>` that says `This is a list of tourist attractions for` followed by the state name with the `title` filter.
Once this is added, go ahead and click on one of the state details buttons to see what this page looks like!

16. This page is going to look similar to the homepage.
Start by adding a table with the headers _Attraction_ and _State_ to the content block.

17. We still want to go through each attraction. Therefore, create a loop similar to the one from before that goes through every item in `attractions`. This loop should also use the `dictsort:"state"` filter.

18. One thing we want to do differently here is that we only want to display attractions in the selected state. We know what state we want to use because we have a variable called `statename` passed in from **views.py**.
To do this, we are going to want to add an `if` statement that checks to see if the attractions state is the same as `statename`. However, we need to add the `lower` filter to the attractions state since that is capitalized, but `statename` is not capitalized.

19. Inside of the `if` statement, add a table row with two table details. One displaying the attraction name and the other displaying the attraction state.
If done correctly, when you click on the “State details” link, you’ll get linked to a page that only displays that state’s attractions!

20. And that’s it! We now have a website that displays attractions for any state! Go ahead and modify views.py to add more states and see how our templates react! If you want, go ahead and try to add an image on the homepage!
