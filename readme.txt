
CascadingDropDown : a jQuery plugin, version: 0.2 (2010-05-21)
@requires jQuery v1.4 or later

CascadingDropDown is a jQuery plugin that can be attached to a select list to get automatic population. 
Each time the source element changes value, an ajax request is made to retrieve a list of values for 
the select list. The respose from the ajax request should be in json with the following format

   [{
       "Text": "John",
       "Value": "10326"
   },
   {
       "Text": "Jane",
       "Value": "10801"
   }] 

Details:

$(targetID).CascadingDropDown(sourceID, actionPath, settings)

    targetID
      The ID of the select list that will auto populate. 
    sourceID
      The ID of the select list, which, on change, causes the targetID to auto populate.
    actionPath
      The url to post to

Options:

    promptText
      Text for the first item in the select list
      Default : -- Select --
    loadingText
      Optional text to display in the select list while it is being loaded.
      Default : Loading..
    errorText
      Optional text to display if an error occurs while populating the list
      Default: Error loading data.
    postData
      Data you want posted to the url in place of the default
      Example :
      postData: function () {
          return { prefix: $('#txtPrefix').val(), customerID: $('#customerID').val() };
      }
      will cause prefix=foo&customerID=bar to be sent as the POST body.
      Default: A text string obtained by calling serialize on the sourceID
    onLoading (event)
      Raised before the list is populated.
    onLoaded (event)
      Raised after the list is populated, The code below shows how to “animate” the  select list after load.
    defaultValue
      Optional value that you want to be selected after the dropdown is initialized


Example using custom options:

  $("#orderID").CascadingDropDown("#customerID", '/Sales/AsyncOrders',
  {
    promptText: '-- Pick an Order--',
    onLoading: function () {
        $(this).css("background-color", "#ff3");
    },
    onLoaded: function () {
        $(this).animate({ backgroundColor: '#ffffff' }, 300);
    }
  });

Licensed under the MIT:
http://www.opensource.org/licenses/mit-license.php

Raj Kaimal http://weblogs.asp.net/rajbk/

v 0.2 Added support for custom postData using functions
