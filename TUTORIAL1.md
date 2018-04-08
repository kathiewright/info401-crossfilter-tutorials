Tutorial 1
==========================

This tutorial contains examples of data manipulation using the **crossfilter.js** library.  You can find out more about the [crossfilter.js API in GitHub.](https://github.com/crossfilter/crossfilter/wiki/API-Reference).

We are going to do all the work in this tutorial in the index.html file as in-line JavaScript code.

Tutorial Steps
------------

**Setup:**  Let's set up the crossfiltered data by adding the data array from data.js into the Crossfilter function.  Then we print it out 2 ways:  as a console.log statement and using the print_filter commmand

   Code Snippet:

       var facts = crossfilter(data);
         //console.log(facts);   //displays facts as a set of objects
        print_filter('facts');  //displays facts as a set of data

**Exercise 1:** This code snippet creates a dimension on the order number.  Note that  each order may contain 1-4 different products, so there may be multiple 'facts' for a single order to reflect the number of products.  Once the data is dimensioned on the order field, it is possible to group the data based on the order number and then reduce the count of the facts to reflect unique order numbers. 

  Code Snippet:

      var orderDimension = facts.dimension(function(d){return d.order;});
          console.log("Total Number of Unique Orders");
          print_filter('orderDimension.group().reduceCount()');

**Exercise 2:** Now let's do a similar dimension on team.  The output in the console should show the 7 teams each with the number of facts associated with that team.

  Code Snippet:

      var teamDimension = facts.dimension(function(d){return d.team;});
      console.log("Team Dimension");
      print_filter('teamDimension.group().reduceCount()'); 
      
**Exercise 3:** This one is a bit different from the multi-dimension code shown in the video, although it is based on the Lynda exercise files that came with the course.  In this code, we are dimensioning the data on two fields:  area and value.   "d.area" categorizes the facts by  region (North, South and West) and "d.value" sorts the values from highest to lowest.  Note that in printing out the dimension, an additional command, "top(3)" is added to limit the values to the top 3.

  Code Snippet:

      var areaDimension = facts.dimension(function(d){ return [d.area, d.value]; }); 
      console.log("Top 3 Orders in the West");
      print_filter('areaDimension.top(3)');
      
**Exercise 4:** A problem with the previous example is that it doesn't really filter the data
it is just that the dimension function sorts the dimensions in descending order, so the 
"WE" or West region is the top set of records.  In this example, we are going to use a filter 
on data that has been dimensioned by team.  

  Code Snippet:

      var areaDimension = facts.dimension(function(d){ return d.team; }); 
      areaDimension.filter('DD');
      print_filter('areaDimension');
      
This will result in 213 records where the value of team is DD.  Now, let's say that we want to order
those records by the quantity that was purchased.  Once a filter has been set, it remains in place
on all subsequent commands until the .filterAll() command removes it.  So we will take 
advantage of the team filter and create a secondary index based on the quantity that is purchased.

  Code Snippet:

      var qtyDimension = facts.dimension(function(d){return d.quantity;});
          console.log("Transactions for Team DD Ordered by Quantity");
          print_filter('qtyDimension');
          console.log("Top 3 Sales by Quantity for Team D");  
          print_filter('qtyDimension.top(3)');  _filter('areaDimension');