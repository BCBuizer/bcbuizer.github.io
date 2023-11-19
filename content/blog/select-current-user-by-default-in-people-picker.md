+++
title = 'Select Current User by Default in People Picker'
date = 2023-11-19T15:32:05+01:00
draft = false
+++

In case you are building a canvas app in Power Apps and you need to have the current user selected in a people picker combobo box by default, this is a quick and easy way to achieve this.

## Create a people picker combobox
First insert a combo box control in your app and set its' **Items** property to:
```
Choices(DataSource.PersonTypeColumn)
```
In the above formula *DataSource* referes to data source such as a Dataverse table or SharePoint list and *PersonTypeColumn* refers to a column inside that data source which is of type Person/Group. 

The next step is to make sure the combo box is displaying the information by selecting **Edit** next to **Fields** in the properties pane on the left side of Power Apps studio, selecting the **Person** option under **Layout** and making sure the relevant columns are selected for **Image**, **Primary text** and **Secondary text**.

![Screenshot of the Power Apps studio showing how to set up a people picker comobobox as explained in the text before the screenshot.](/images/PeoplePicker.PNG "How to set up a peoplepicker combobox.")

## Selecting the current user by default
The same `Choices()` function can be used to select the current user by default in the **DefaultSelectedItems** property of the people picker combo box:
```
First(Choices(DataSource.PersonTypeColumn, User().Email))
```
By using the `User()` function in the second argument of the `Choices()` function, the possible values are filtered, returning only those that match the email address of the current user. To then convert the returned table into a single record, the `First()` function is used.

As a result, whenever the people picker combo box is reset, the current user is selected:

![Screenshot of the Power Apps studio, showing the result of the above text on how to set .](/images/PeoplePickerUserDefault.PNG "Select current user by default in a peoplepicker combobox")

## Added benefit
In some cases the DisplayName column will contain a different value than what `User().FullName` returns. An added benefit of this method over other methods is that a consistant value for the displayname of the current user is displayed.