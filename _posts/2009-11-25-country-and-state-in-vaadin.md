---
title: Country and State in Vaadin
author: mnash
layout: post
permalink: /country-and-state-in-vaadin/
related_exlink_1:
  - 
related_exlink_1_desc:
  - 
related_exlink_2:
  - 
related_exlink_2_desc:
  - 
related_exlink_3:
  - 
related_exlink_3_desc:
  - 
related_exlink_4:
  - 
related_exlink_4_desc:
  - 
related_exlink_5:
  - 
related_exlink_5_desc:
  - 
categories:
  - Software Craftsmanship
tags:
  - Select
  - Vaadin
  - webapp
---
In my ongoing tinkering with the Vaadin web framework, I had a need to build a country and state/province dropdown, much like you see on almost every e-commerce site out there.

Unlike the typical pair of these fields, however, I wanted mine to work correctly &#8211; that is, for the list of provinces or states to reflect the currently selected country automatically.

Simple as this sounds, it&#8217;s an exercise I&#8217;ve done many many times in too many different frameworks and technologies to count, and it&#8217;s never quite as easy it as seems like it ought to be. As you can see, many sites give up, and simply have a combined list of all states and Canadian provinces, or some such hack. I&#8217;ve never actually seen one that changes the name of the &#8220;State&#8221; field to &#8220;Province&#8221; when Canada is selected as the country, for instance.

So I set out to try this in Vaadin, and was pleasantly surprised. 

Let&#8217;s assume we&#8217;re building a Form object in Vaadin. We can add our &#8220;country&#8221; drop down select box by saying this:

<div class="capsule" style="text-align: left">
  <pre>
 &lt;code&gt;
        Select country = new Select("Country:");
        country.addItem("[Unspecified]");
        country.addItem("United States");
        country.addItem("Canada");
        country.addItem("Afganistan");
        form.addField("country", country);
&lt;/code&gt;
</pre>
</div>

Of course, we&#8217;d probably want our list of countries to come from some other data source, like a property file or static list, but this gives you the idea.

Now we add our &#8220;state&#8221; drop-down:

<div class="capsule" style="text-align: left">
  <pre>
 &lt;code&gt;
        final Select state = new Select("State:");
        form.addField("state", state);
&lt;/code&gt;
</pre>
</div>

Now we must decide whether to populate the state with actual U.S. States or Canadian provinces&#8230;.

<div class="capsule" style="text-align: left">
  <pre>
 &lt;code&gt;
        country.addListener(new Property.ValueChangeListener() {
            public void valueChange(Property.ValueChangeEvent valueChangeEvent) {
                String selectedCountry = valueChangeEvent.getProperty().getValue().toString();
                if (selectedCountry.equals("United States")) {
                    state.setCaption("State:");
                    state.removeAllItems();
                    state.addItem("Alabama");
                    state.addItem("Texas");
                    state.addItem("Idaho");
                } else if (selectedCountry.equals("Canada")) {
                    state.setCaption("Province:");
                    state.removeAllItems();
                    state.addItem("Alberta");
                    state.addItem("Saskatchewan");
                    state.addItem("Manitoba");
                }
                state.requestRepaint();
            }
        });
&lt;/code&gt;
</pre>
</div>

So our fields before we select a country look like this:  
![country state1 Country and State in Vaadin][1]

Now we&#8217;ve got a &#8220;state&#8221; field that will change it&#8217;s title to &#8220;Province:&#8221; if the country we select is Canada, and populate itself with the appropriate list of the provinces.  
![country state canada selected Country and State in Vaadin][2]

But switch right back to &#8220;State&#8221; and populate the dropdown accordingly if we change our minds and select United States again&#8230;

![country state back to state Country and State in Vaadin][3]

Not too difficult, and very easy to understand and extend to other situations (or countries). 

As with all Vaadin, it&#8217;s pure Java, fully testable (at the Unit level, as well as at the functional level). In fact for the &#8220;real&#8221; version of this (which reads it&#8217;s countries and such from property files), I was even able to easily TDD it, which often isn&#8217;t the case in UI technologies.

<div class="g-plusone" data-annotation="inline" data-width="300">
</div>

<!-- Place this tag after the last +1 button tag. -->

  


<div class="st-callout hastitle lightblue center" >
  <h4 class="st-callout-title ">
    Principles and Practices
  </h4>
  
  <div class="inside">
    <i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book: <a href="http://jglobal.com/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="http://jglobal.com/dispatches/">Craftsmanship Dispatches</a> newsletter.
  </div>
</div>

<div class="clear">
</div>

 [1]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/country-state1.jpg "Country and State in Vaadin"
 [2]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/country-state-canada-selected.jpg "Country and State in Vaadin"
 [3]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/country-state-back-to-state.jpg "Country and State in Vaadin"