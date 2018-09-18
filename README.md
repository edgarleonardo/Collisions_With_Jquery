# Draggable and Collision With Jquery

In this article I am going to explain with a single example how make a collision between two div using draggable to move put a div over others and once those div touch each other then the static one become part of the draggable one.

We are going to use an html that is publish on my github for any consulting, in that html we are going to see four divs, three static and motionless and the other one dynamic using Draggable component of the Jquery Library.

Image Examples:

![This is how the html looks like once we refresh the page](https://raw.githubusercontent.com/edgarleonardo/Collisions_With_Jquery/master/image1.jpg)

![This is how the html looks like once a littler div is swallowed](https://raw.githubusercontent.com/edgarleonardo/Collisions_With_Jquery/master/image2.jpg)


![This is how the html looks like once a second div is swallowed](https://raw.githubusercontent.com/edgarleonardo/Collisions_With_Jquery/master/image3.jpg)


![This is how the html looks like once a third div is swallowed](https://raw.githubusercontent.com/edgarleonardo/Collisions_With_Jquery/master/image4.jpg)


## A Bit Explanation

To be able to know when a div reach other we need to calculate current position in pixels of each divs and compare with the other.

For example, imagin we have two divs located on different the positions:

**Div1**
Top = 10px
Left = 5px

**Div2**
Top = 10px
Left = 5px

In order to be able to know the real amount of px that a component has on the screen we need to add the heigh and the width in the calculation.

**Div1**
Width = 20px
Height = 20px

**Div2**
Width = 30px
Height = 30px

To now wheather the two divs collide, we need to calculate the onscreen position of each divs.

In order to make the calculation, we need to know the screen height and width of each component on screen.

For that, we are going to calculate the Screen Height as:

***Screen Height = Height + Top***

And the Screen Width as :

***Screen Width = Width + Left***

So, now let's calculate the information needed with the formula from above:

**Div1**
Screen Height = 20px + 10px = 30px
Screen Width = 20px + 5px

**Div2**
Screen Height = 30px + 10px = 40px
Screen Width = 30px + 5px = 35px

Now let's get how success looks like when the two divs objects collide each others.

When **Div1**:Screen Height is equal to the **Div2**:Top
When **Div1**:Screen Width is equal to **Div2**:Left
When **Div2**:Screen Height is equal to the **Div1**:Top
When **Div2**:Screen Width is equal to **Div1**:Left
 
Following the above, below is the function using Jquery:

`function calculateCollition($draggableDiv, $obstacleDiv) {
        var x1 = $draggableDiv.offset().left;
        var y1 = $draggableDiv.offset().top;
        var h1 = $draggableDiv.outerHeight(true);
        var w1 = $draggableDiv.outerWidth(true);
        var b1 = y1 + h1;
        var r1 = x1 + w1;
        var x2 = $obstacleDiv.offset().left;
        var y2 = $obstacleDiv.offset().top;
        var h2 = $obstacleDiv.outerHeight(true);
        var w2 = $obstacleDiv.outerWidth(true);
        var b2 = y2 + h2;
        var r2 = x2 + w2;
        if (
            b1 < y2 || 
            y1 > b2 || 
            r1 < x2 || 
            x1 > r2
        ) return false;
        return true;
      }`

This function check two divs and make the calculation we made before and return true when the collision occured and false when don't.

Now let's add the behavior to our Draggable function: 

`$(containerclass).draggable({
    containment: "document",
    drag: function(event, ui) {
        var draggableDiv = $(this);
        $(collitionClass).each(function( index, div ) {
        if (calculateCollition(draggableDiv, $(div)))
        {
            var newDiv = $('<div  class="finalComponent" style="position:relative;"></div>');
            $(div).css({'display': 'none'}); 
            $( ".container").append(newDiv );
        }
});
    },
    stop: function(event, ui) {
    }
});`

Now we are able to see the example explained at the beginning of this article and how each div get swallowed by the bigger like we wanted to see.

Here is the repository.

Have fun.
