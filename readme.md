wip

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
 "post_status" => "publish",
))
```

## AJAX Endpoints
Admin AJAX API calls should be used for most of the backend administration.

Get specific message as JSON object.
GET     /wp-admin.php?action=/message/23432

Delete a message by ID.
DELETE  /wp-admin.php?action=/message/23432

Perform basic search/query.
GET     /wp-admin.php?action=/messages?q=type:critical

Mark a message as acknowledge
GET    /wp-admin.php?action=/message/23432/acknowledge

Mark a message as accepted
GET    /wp-admin.php?action=/message/23432/accept

Mark a message as rejected
GET    /wp-admin.php?action=/message/23432/reject


