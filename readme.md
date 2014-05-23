There is a growing need to be able to notify or engage select users in regards to certain web services. Specifically, there is often a need to notify the user while they are using their WordPress control panel - such as in the case of a third-party service being used by the CMS on behalf o the user requiring re-authentication.

Additionally, there is a growing need to keep users updated on non-critical messages related to their ongoing web services, such as data syndication. Delivering such messages over e-mail is not nearly as ideal as in the control panel where where the user take the necssary action to resolve the issue, acknowledgement a change or reject an update of some sort.

## Objectives
- Allow a standard way of pushing messages to WordPress sites over XML-RPC. 
- Allow for basic Acknowledgement, Acceptance and Rejection of messages.
- Display Critical notifications that may be affecting service availability in the administrative toolbar.
- Deliver non-administrative messages to website users who choose to subscribe to a particular topic of interest. 

## Basic Message Manipluation
```php
// Get Message by ID.
$message = new UsabilityDynamics\Message( 23454302133 );

// Mark Message as Read.
$message->read();

// Acknowledge Receipt.
$message->acknowledge();

// Archive.
$message->archive();

// Delete Permanently.
$message->delete();
```

## Message Queries
Single Messages are Post Types they have all the same searching and querying functionality as Posts and Pages.

```php
$messages = get_posts(array(
 "post_type" => "_message",
 "post_status" => "publish"
));

// Query for critical messages related to a particular application - e.g. WP-Property XML-Importer.
$messages = UsabilityDynamics\Messages\Query(array(
  "type": "critical",
  "app_id": "wpp.xmli"
));

// Query all messages that have not been ready AND require acknowledgement.
$messages = UsabilityDynamics\Messages\Query(array(
  "mustAcknowledge": true,
  "read": false
));

```

## AJAX Endpoints
Admin AJAX API calls should be used for most of the backend administration.

Get specific message as JSON object.
* ```GET     /wp-admin.php?action=/message/23432```

Delete a message by ID.
* ```DELETE  /wp-admin.php?action=/message/23432```

Perform basic search/query.
* ```GET     /wp-admin.php?action=/messages?q=type:critical```

Mark a message as acknowledge
* ```GET    /wp-admin.php?action=/message/23432/acknowledge```

Mark a message as accepted
* ```GET    /wp-admin.php?action=/message/23432/accept```

Mark a message as rejected
* ```GET    /wp-admin.php?action=/message/23432/reject```

## Future / Low Priority Features
* Ability for messages to make XML-RPC callbacks (reply_to) back to the service that was needing an action once an action is made by user.
* Allow messages to be used within plugins and themes to deliver product-related updates in a branded manner.


## License

(The MIT License)

Copyright (c) 2013 Usability Dynamics, Inc. &lt;info@usabilitydynamics.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
