---
maintainer:lakruzz
---

# GoogleMailFilters
My Google mail filters - as code

These are my mail filters that I use to keep my mailbox tidy.

I get roughly 150 mails per day, most of them are notifications from collaboration platforms that I'm using: GitHub, Google, Twitter, Slack, Meetup, Trello, Fogbugz, Linkedin...

I classify theses as _Notifications_ meaning that the all information I get from here, is something that is _also_ stored somewhere else. These are mails that I consider safe to delete (as opposed to archive) when I've read them.

Filters in this repo are `xml` and they are all initially created simply by making the filter in my Google mail (`setting -> Filters and blocked addresses -> ...`) and then exporting it.

I've created individual files for each individual source I'm filtering on. This way the filters might prove more useful to others as well - Each file may contain more than one filter, but they are then all related to the same source.

## The rationale

The principles I'm using in my filters are these:

* All mails that - after filtering - remains unread in my inbox gets my undivided attention.
* I empty my inbox _every single day_.
* Everything that doesn't deserve my undivided attention should be filtered. I'll apply it with a label and archive it immediately - but I'll keep it marked as _unread_.
* I read (and delete) all my unread mails regularly, typically as part of my daily afternoon or evening routines.

Following these principles I filter on the notification sources I receive mails from, label them `Notification/xxx` and bypass the inbox.

__Except__  notifications where my user handle is mentioned!

They should stay in my inbox, unread and not labeled as notifications - This way they get my undivided attention.

### Example

_Mentioning my user handle in a commit our issue on GitHub, will have the same effect as sending me a personal direct email._

The way this is implemented is through filters in pairs of two, where one is the exact negation of the other. Like this one I use for GitHub:

    <!-- Captures notifications from GitHub that mentions @lakruzz -->
    <apps:property name='from' value='notifications@github.com'/>
    <apps:property name='hasTheWord' value='&#64;lakruzz'/>
    <apps:property name='label' value='Mention'/>

The filter is then match with another one, that uses the _exact_ same value as defined in the `hasTheWord` property, but this time applied to the `doesNotHaveWord` property.

    <!-- Captures notifications from GitHub that doesn't mention @lakruzz -->
    <apps:property name='from' value='notifications@github.com'/>
    <apps:property name='doesNotHaveTheWord' value='&#64;lakruzz'/>
    <apps:property name='label' value='Notification/Github'/>
    <apps:property name='shouldArchive' value='true'/>

The first one leaves messages that mentions me unread in the inbox, the second one archives them directly, but still leaves them unread.
