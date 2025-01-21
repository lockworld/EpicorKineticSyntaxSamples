# Creating a text box with a search field

## Epicor Versions:

* 2023.1


## Overview

In this demo, we will add a text box to a Kinetic application and configure it to use a built-in Epicor search to search for a Part Number, which will then be populated into the text box on our form.

## Important Notes

1. You need to have the text box bound to a field in a DataView for this to work.

## Instructions

Add a text box to your Kinetic application and bind it to a column in a DataView available in your app:

![Screenshot of a Kinetic application with a simple text box. The Properties window is displayed, with the "Data" section expanded. A binding to "App01Data.PartNum" has been entered in the EpBinding field in the Data section](../_resources/TextBoxWithSearch/2025-01-21_16-09-36-798_brave_App_-_Brave.png)

Check the "Enable Search" checkbox:

![Screenshot of a Kinetic application with a text box highlighted and the "Properties" panel open. The checkbox labeled "Enable Search" is checked](../_resources/TextBoxWithSearch/2025-01-21_15-41-27-445_brave_App_-_Brave.png)


Scroll back up in the Properties window, expand "Behavior" and click "On Search Click":

![Screenshot of a Kinetic application's properties window showing the "Behavior" section expanded and the "On Search Click" button](../_resources/TextBoxWithSearch/2025-01-21_15-58-46-649_brave_App_-_Brave.png)

Epicor will create a new event and bind it to the on-click event for the DataView field your search box is bound to:

![Screenshot of a Kinetic application showing an event named "App01Data.PartNum_onClick" with a trigger configured using Type=EpBinding, Hook=OnClick and Target=App01Data.PartNum](../_resources/TextBoxWithSearch/2025-01-21_16-13-54-716_brave_App_-_Brave.png)

Open the "Toolbox" tab and type "search" in the search box. You will see two search components that can be added:

![Screenshot of a Kinetic application showing an event named "App01Data.PartNum_onClick" with the toolbox open and the work "search" typed into the search box. Below the search box are two components named "search-value-set" and "search-show"](../_resources/TextBoxWithSearch/2025-01-21_16-15-25-098_brave_App_-_Brave.png)

First, drag the "search-show" component into the event editor so that it connects. Open the Properties panel and click on the "Parameters" option under the "Basic" heading:

![Screenshot of a Kinetic application showing an event named "App01Data.PartNum_onClick" with the "search-show" element added to the editor and the properties window open, revealing the "Parameters" button](../_resources/TextBoxWithSearch/2025-01-21_16-17-33-832_brave_App_-_Brave.png)

Click on the "Search Options" button in the Parameters window to reveal the search options. In the "Like *" column, you will need to type the name of an Epicor search. Epicor does not provide a list of acceptable values to put here, nor provide information on how to determine what values are valid. Instead, the name of the field is "Like *" and the _extremely_ helpful tooltip text is "Set the like property of the search form."

![Screenshot of a Kinetic application showing an event named "App01Data.PartNum_onClick" with the "properties" window open to "search-show" => "Parameters" => "Search Options." The properties are all blank, and the cursor is hovering over the field named "Like *" and showing a tooltip preview that reads "Set the like property of the search form."](../_resources/TextBoxWithSearch/2025-01-21_16-26-03-657_brave_App_-_Brave.png)

Since none of that is remotely helpful, I will provide an example of how to add a search for a Part Number, and leave it up to you to figure out how to add the appropriate value here to get the proper search set up.

Despite the use of the term "Like" in this field, you will need to enter the exact text necessary to configure a very specific search.

To get our search working, we only need to pick a "Select Mode" from the dropdown (SingleSelect) and enter the exact, precise, absolute, complete name of what we are searching for in the "Like *" column. In our case, we are looking in the Part table for a Part Number, so we will enter **Part.PartNum** here:

![Screenshot of a Kineti application showing an event named "App01Data.PartNum_onClick" with the "Properties" window open to "search-show" => "Parameters" => "Search Options." The "SelectMode" property has been set to "SingleSelect" and the "Like *" property has been set to "Part.PartNum"](../_resources/TextBoxWithSearch/2025-01-21_16-29-16-701_brave_App_-_Brave.png)

This is enough to cause the search panel to slide open and allow the user to search for and select a Part Number from the list. But we still need to store the value the user selected into our DataView field.

In the toolbox window, enter "search" in the search box to display a list of available components to add to our event:

![Screenshot of a Kinetic application showing an event named "App01Data.PartNum_onClick" with the toolbox open and the word "search" typed into the search box. Below the search box are two components named "search-value-set" and "search-show"](../_resources/TextBoxWithSearch/2025-01-21_16-15-25-098_brave_App_-_Brave.png)


Drag the "search-value-set" component into the event editor so that it connects to the "search-show" event. Switch to the "Properties" tab and enter the DataView.Field that you want to **store the value it** in the **EpBinding** field. Then enter **searchResult.PartNum** in the **Value** field. The **searchResult** object is a built-in system DataView available on any Kinetic application. The **PartNum** field is populated from the search reselt the user selected in the search panel. If you are using a different search, you will need to set the correct field name for the row that was selected in the search.

![Screenshot of a Kinetic application showing an event named "App01Data.PartNum_onClick" with the "search-value-set" object selected and the "Properties" window open. The field labeled "EpBinding" contains the text "App01Data.PartNum" and the field labeled "Value" contains the text ""searchresult.PartNum."](../_resources/TextBoxWithSearch/2025-01-21_16-36-15-126_brave_App_-_Brave.png)

Save the app and click the "Preview" button to test the application:

![Animated gif showing our application in AppStudio. The user clicks on the "Save" icon and then the "Preview" icon. The application loads a blank page with a text box labeled "PartNum." The user clicks the "Search" icon inside the text box and a search panel is opened, showing options for a Part search. The user types "M2S" into the "Starting at" field in the search panel and clicks "Search." The application loads a set of part numbers beginning with "M2S" into the search results. The user checks a checkbox on one of the rows containing the Part Number "M2SXXX" and clicks "OK" on the search panel. The search panel closes, and the selected part number is populated in our text box.](../_resources/TextBoxWithSearch/2025-01-21_16-45-08-367_brave_App_-_Brave.gif)
