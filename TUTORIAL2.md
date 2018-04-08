Tutorial 2
==========================

This tutorial contains examples of data manipulation using the Group commands

Tutorial Steps
------------

**Exercise 1:** This code snippet creates a dimension on the team designation which is then grouped and assigned to the variable **teamGroup**.  This enables you to use the reduceSum() and reduceCount() functions directly on the variable teamGroup.  Note that the first print command displays the number of records in each team group (essentially replicating a .reduceCount() function.  The second two commands roll up the sales value and quantity sold for each team respectively.

  Code Snippet:

        var teamDimension = facts.dimension(function(d){ return d.team; });   
        var teamGroup = teamDimension.group();
        print_filter('teamGroup');      
        print_filter('teamGroup.reduceSum(function(d){return d.value})');
        print_filter('teamGroup.reduceSum(function(d){return d.quantity})');   

**Exercise 2:** Now let's try a similar exercise on a two dimension grouping.  Note the affect on the key which is now a composite of the team and the area (NO, SO, WE).

  Code Snippet:

      var teamDimension = facts.dimension(function(d){ return [d.team, d.area]; });  

      var teamAreaGroup = teamDimension.group();
          print_filter('teamAreaGroup');

          print_filter('teamAreaGroup.reduceCount(function(d){return d.value})');
      
