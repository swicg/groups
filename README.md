# Groups

This is a task force of the [Social Web Incubator Community Group (SWICG)][swicg] to explore the use of groups in ActivityPub.

## Leads

The task force leads are [Evan Prodromou](https://github.com/evanp) and [a](https://github.com/twrnh).

## User stories

[User stories](https://en.wikipedia.org/wiki/User_story) for this task force are collected and tracked in the [GitHub issue tracker][issues]. Each user story issue has the [user story issue tag][user story issue tag].

- [Join a group][1] "As an ActivityPub user, I want to join a group, so I can be part of it."
- [Leave a group][2] "As an ActivityPub user, I want to leave a group I'm a member of, so I no longer have the responsibilities of group membership."
- [Create a group][3] "As an ActivityPub user, I want to create a group, so I can be part of it and people can join it."
- [Invite to a group][4] "As an ActivityPub user, I want to invite someone to a group, so they know of a good group to join."
- [Expel from a group][5] "As a group administrator, I want to expel a member from a group, so that they can no longer participate as a member."
- [Get list of members][6] "As an ActivityPub user, I want to get a list of members of a group, so I can know if it's a group I'd like to join."
- [Get list of admins][7] "As an ActivityPub user, I want to get the list of admins for a group, so I can see who can do special chores for the group that other members can't."
- [Invite to admin][8] "As a group owner, I would like to invite a group member to become an admin, so they can help with moderation and other tasks."
- [Expel an admin][9] ""As a group owner, I want to expel an admin, so they no longer have special privileges with respect to a group."
- [Accept a Join request][10] "As a group admin, I would like to accept a Join request to a group, so that the actor becomes a member of the group."
- [Reject a Join request][11] "As a group admin, I want to reject a Join request to a group, so that the actor does not become a member."
- [Post content publicly][12] "As a group member, I want to post content that is distributed to all the other members of the group and is also visible to the public, so that people in the group can reshare it to others."
- [Post content privately][13] "As a group member, I want to post content that is visible to the group members only, so that we can have a private discussion."
- [Get a stream of the content that was posted to the group members][14] "As an ActivityPub user, I want to see a feed of content that was posted to the group, so I can get an idea of what kind of content is posted there." "As a group member, I want to see a feed of content that was posted to the group, so I can catch up with the latest posts."
- [Close a group][16] "As a group owner, I want to close down a group, either because it's become terrible, or because it no longer has a purpose."
- [Add to a group collection][18] "As a group member, I want to add content to a group collection such as a document base or a photo album, so others can view the items in the collection."
- [Remove from a group collection][19] "As a group member, I want to remove some content from a group collection, because it's no longer good to share that content in the group."
- [Transfer group ownership][20] "As a group owner, I want to transfer ownership to another actor, so I no longer have the responsibilities of group ownership."
- [Get group info][21] "As an ActivityPub user, I want to get information about the group such as its name, description, illustrative image, or other properties, so I can understand what the group is for and how it works."
- [Change group info][22] "As a group owner, I want to change information about the group such as its name, description, image, or other properties, so that others can understand the group."
- [Moderate group posts][23] "As a group admin, I want to review posts made to the group before they are distributed, so I can make sure they are on topic and match the group's expected conduct."

## What is a group?

The English word "[group](https://en.wikipedia.org/wiki/Group)" has many different meanings in different contexts. In social networks, it has two usual meanings:

- A collection of people or other kinds of actors, curated by a single actor. The collection helps the actor keep track of certain kinds of actors they have contact with, such as friends from college, family members, neighbours, or coworkers. The collection can be public or private. The actor can add or remove actors from the collection without their consent. Other names: lists, contact lists.
- An opt-in collection of actors that want to communicate with each other. Actors choose to join or leave the collection. Some metadata about the collection is usually public, to allow actors to make informed decisions about joining or leaving. When sharing information with the collection, actors don't have to enumerate all the members of the collection when addressing.

This task force is focused on the second meaning of "group". The user stories above define behaviours that are expected of a group in this sense.

## Group representation

Groups are represented by an [ActivityPub object](https://www.w3.org/TR/activitypub/#obj) with object type [Group](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-group).

Important properties of a group include:

- `id`: The unique identifier of the group. This is usually a URL.
- `type`: The type of the object. For groups, this is `Group`; with multi-typing, this can be a list of types.
- `name`: The name of the group. This is usually a short string.
- `summary`: A short description of the group. This is usually a short string.
- `image`: An image that represents the group. This is usually a [Link](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-link) object, an [Image](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-image) object, or an array of Image or Link objects.
- `icon`: A small, usually square image that represents the group. This is usually a [Link](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-link) object, an [Image](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-image) object, or an array of Image or Link objects.

There are other properties mentioned in the user stories that have reasonable implementations as group. These properties can be included in JSON-LD documents using the [https://swicg.github.io/groups/0.1.0.jsonld](https://swicg.github.io/groups/0.1.0.jsonld) context.

- `members`: An [OrderedCollection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-orderedcollection) representing the members of the group. This is a collection of [ActivityPub actors](https://www.w3.org/TR/activitypub/#actors) that have joined the group. The collection is ordered in reverse-chronological order, with the most recent member first.
- `admins`: An [OrderedCollection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-orderedcollection) representing the admins of the group. This is a collection of [ActivityPub actors](https://www.w3.org/TR/activitypub/#actors) that have been given special privileges in the group. The collection is ordered in reverse-chronological order, with the most recent admin first.
- `collections`: An [OrderedCollection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-orderedcollection) representing the collections of the group. This is a collection of [Collection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-collection)s that have been added to the group. Each collection contains ActivityPub objects, such as [Images](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-image), [Document](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-document), or [Articles](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-article). The collection is ordered in reverse-chronological order, with the most recent collection first.
- `pendingActivities`: An [OrderedCollection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-orderedcollection) representing the queue of activities that have been posted to the group and not yet redistributed to the members.
- `pendingMembers`: An [OrderedCollection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-orderedcollection) representing the queue of join requests that have been sent to the group and not yet accepted or rejected by the admins.

The "owner" relationship can be represented with the [attributedTo](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-attributedto) property. The owner of the group is the actor that created the group. The owner can be a member of the group, but does not have to be.

❓ **Question:** Should the `Group` be an [ActivityPub actor](https://www.w3.org/TR/activitypub/#actors), including an [inbox](https://www.w3.org/TR/activitypub/#inbox) and [outbox](https://www.w3.org/TR/activitypub/#outbox)? Actors can receive activities and act on them directly. Some of the implementation options for posting to groups require the group to be an actor that can receive and then redistribute activities.

An example group:

```json
{
  "@context": [
    "https://www.w3.org/ns/activitystreams",
    "https://swicg.github.io/groups/0.1.0.jsonld"
  ],
  "id": "https://example.com/groups/world-group",
  "type": "Group",
  "name": "World Group",
  "summary": "A group of people who want to talk about the world.",
  "image": {
    "type": "Link",
    "href": "https://example.com/images/world-group.jpg"
  },
  "icon": {
    "type": "Link",
    "href": "https://example.com/images/world-group-icon.jpg"
  },
  "members": {
    "type": "OrderedCollection",
    "id": "https://example.com/groups/world-group/members"
  },
  "admins": {
    "type": "OrderedCollection",
    "id": "https://example.com/groups/world-group/admins"
  },
  "collections": {
    "type": "OrderedCollection",
    "id": "https://example.com/groups/world-group/collections"
  },
  "pendingActivities": {
    "type": "OrderedCollection",
    "id": "https://example.com/groups/world-group/pendingActivities"
  },
  "pendingMembers": {
    "type": "OrderedCollection",
    "id": "https://example.com/groups/world-group/pendingMembers"
  },
  "attributedTo": {
    "id": "https://example.com/actors/3456789012",
    "type": "Person",
    "name": "Evan Prodromou"
  }
}
```

## Protocol

The following sections describe the protocol for groups.

### Posting content to a group

To post content to a group, the actor sends an [ActivityPub Create](https://www.w3.org/TR/activitypub/#create) activity to the group. The activity must include the `object` property, which is the content to be posted. The content can be any ActivityPub object, such as an [Image](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-image), [Note](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-note), or [Video](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-video).

An example activity posted to a group ([Post privately to a group][13])

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Create",
  "object": {
    "id": "https://example.com/notes/2345678901",
    "type": "Note",
    "content": "Hello, world!"
  },
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  }
}
```

The `to` property of the activity is a [Group](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-group) actor that represents the group.

The `Group` actor is responsible for redistributing the activity to all the members of the group.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/groups/world-group/activities/1234567890",
  "type": "Announce",
  "actor": "https://example.com/groups/world-group",
  "to": "https://example.com/groups/world-group/members",
  "object": {
    "id": "https://example.com/activities/1234567890",
    "actor": "https://example.com/actors/3456789012",
    "type": "Create",
    "object": {
      "id": "https://example.com/notes/2345678901",
      "type": "Note",
      "content": "Hello, world!"
    },
    "to": {
      "type": "Group",
      "id": "https://example.com/groups/world-group",
      "name": "World Group"
    }
  }
}
```

The `Group` actor creates an [Announce](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-announce) activity to redistribute the activity to all the members of the group. The `to` property of the activity is the [OrderedCollection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-orderedcollection) that represents the members of the group.

❓ **Question:** Do the permissions of the `Note` extend to all actors in the members collection, or just the group actor? Should the posting member also include the members collection in addressing?

To post content to a group publicly ([Post publicly to a group][12]), the same flow occurs, but the `to` property of the original activity includes the [Public](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-public) collection.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/3141592653",
  "actor": "https://example.com/actors/27182818284",
  "type": "Create",
  "object": {
    "id": "https://example.com/notes/141592653",
    "type": "Note",
    "content": "Hello, world and public!"
  },
  "to": [
    {
      "type": "Group",
      "id": "https://example.com/groups/world-group",
      "name": "World Group"
    },
    "as:Public"
  ]
}
```

The `Group` actor creates an [Announce](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-announce) activity to redistribute the activity to all the members of the group and the public.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/groups/world-group/activities/3141592653",
  "type": "Announce",
  "actor": "https://example.com/groups/world-group",
  "to": [
    {
      "type": "Group",
      "id": "https://example.com/groups/world-group",
      "name": "World Group"
    },
    "as:Public"
  ],
  "object": {
    "id": "https://example.com/activities/3141592653",
    "actor": "https://example.com/actors/27182818284",
    "type": "Create",
    "object": {
      "id": "https://example.com/notes/141592653",
      "type": "Note",
      "content": "Hello, world and public!"
    },
    "to": [
      {
        "type": "Group",
        "id": "https://example.com/groups/world-group",
        "name": "World Group"
      },
      "as:Public"
    ]
  }
}
```

The `pendingActivities` collection holds activities that have been posted to the group and not yet redistributed. This allows a moderation step, where admins can review the content of posts for topic or tone ([Moderate group posts][23]).

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/groups/world-group/queue",
  "type": "OrderedCollection",
  "attributedTo": "https://example.com/actors/3456789012",
  "to": "https://example.com/groups/world-group/admins",
  "totalItems": 1,
  "items": [
     "https://example.com/activities/1234567890"
  ]
}
```

An admin can view the queue and approve or reject activities before they are redistributed to the members of the group. To accept, they send an `Accept` activity to the group.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/groups/world-group/admins/3456789012",
  "type": "Accept",
  "object": "https://example.com/activities/1234567890",
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  },
  "target": {
    "id": "https://example.com/groups/world-group",
    "type": "Group",
    "name": "World Group"
  }
}
```

To reject, they send a `Reject` activity to the group.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/groups/world-group/admins/3456789012",
  "type": "Reject",
  "object": "https://example.com/activities/1234567890",
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  },
  "target": {
    "id": "https://example.com/groups/world-group",
    "type": "Group",
    "name": "World Group"
  }
}
```

🚪 **Alternative** The above design requires the `Group` to be an actor that can receive activities. Unlike with most ActivityPub structures, the addressing of an activity or object is not directly related to its authorization grants.

An alternative design would have the `Create` activity addressed the group members collection directly.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Create",
  "object": {
    "id": "https://example.com/notes/2345678901",
    "type": "Note",
    "content": "Hello, world!"
  },
  "to": {
    "type": "OrderedCollection",
    "id": "https://example.com/groups/world-group/members",
    "name": "World Group members"
  }
}
```

(Public posts would add `as:Public` as an addressee, as above.) In this alternative, the addressing properties of the activity and the `Note` match the authorization grant, namely, to all members of the group. In this design, however, the actor's server would be responsible for delivering the activity to all members. The activity would not be delivered to the group actor first. This prevents the admins or owner from moderating the content before it is delivered to the group members ([Moderate group posts][23]).

❓ **Question:** Are all activities sent to the group shared with all members? What about activities that are not content focused, such as `Like` or `Question`? What about activities that are part of this protocol, such as `Join` or `Leave`?

### Membership

To get the list of members of a group ([Get list of members][6]), an actor fetches the `members` collection of the group. This will return an `OrderedCollection` object, with information about the members of the group.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/groups/world-group/members",
  "type": "OrderedCollection",
  "totalItems": 2,
  "items": [
    {
      "id": "https://example.com/actors/3456789012",
      "type": "Person",
      "name": "Evan Prodromou"
    },
    {
      "id": "https://example.com/actors/27182818284",
      "type": "Person",
      "name": "a"
    }
  ]
}
```

This collection could be filtered by the authorization of the client, so that only members of the group, or even a more limited set of people, can see the full list.

To join a group ([Join a group][1]), an actor sends a `Join` activity to the group. The activity must include the `object` property, which is the group to join.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Join",
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  },
  "object": {
    "id": "https://example.com/groups/world-group",
    "type": "Group",
    "name": "World Group"
  }
}
```

The owner and/or admins of the group can accept the request ([Accept a Join request][10]). To accept, they send an `Accept` activity to the group, with the `Join` activity as the `object` property.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actor/25418",
  "type": "Accept",
  "object": {
    "id": "https://example.com/activities/1234567890",
    "type": "Join"
  },
  "to": [
    "https://example.com/groups/world-group",
    "https://example.com/actors/3456789012"
  ]
}
```

To reject ([Reject a Join request][11]), an admin sends a `Reject` activity to the group.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actor/25418",
  "type": "Reject",
  "object": {
    "id": "https://example.com/activities/1234567890",
    "type": "Join"
  },
  "to": [
    "https://example.com/groups/world-group",
    "https://example.com/actors/3456789012"
  ]
}
```

To leave a group ([Leave a group][2]), an actor sends a `Leave` activity to the group. The activity must include the `object` property, which is the group to leave.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Leave",
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  },
  "object": {
    "id": "https://example.com/groups/world-group",
    "type": "Group",
    "name": "World Group"
  }
}
```

🚪 **Alternative** The above design requires the `Group` to be an actor that can receive activities. An alternative design would have the actor send the join request to the group's owner and/or admins.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Join",
  "object": {
    "id": "https://example.com/groups/world-group",
    "type": "Group",
    "name": "World Group"
  },
  "to": [
    {
      "id": "https://example.com/actors/3456789012",
      "type": "Person",
      "name": "Evan Prodromou"
    },
    {
      "id": "https://example.com/groups/world-group/admins",
      "type": "OrderedCollection",
      "name": "World Group admins"
    }
  ]
}
```

🚪 **Alternative** The above design for accepting or rejecting `Join` requests could also use the format for `Accept` and `Reject` where a collection is the target, accepting (or rejecting) the joiner into the `members` collection.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/13337",
  "type": "Accept",
  "object": {
    "actor": "https://example.com/actors/3456789012",
    "type": "Person"
  },
  "target": {
    "id": "https://example.com/groups/world-group/members",
    "type": "OrderedCollection",
    "name": "World Group members"
  },
  "to": [
    {
      "id": "https://example.com/groups/world-group",
      "type": "Group",
      "name": "World Group"
    }
  ]
}
```

To invite someone to a group ([Invite to a group][4]), an actor sends an `Invite` activity to actor being invited. The sending actor must have authorization to invite other actors.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Invite",
  "object": {
    "id": "https://example.com/groups/world-group",
    "type": "Group",
    "name": "World Group"
  },
  "target": {
    "type": "Person",
    "id": "https://example.com/actors/27182818284",
    "name": "Non-member"
  },
  "to": {
    "type": "Person",
    "id": "https://example.com/actors/27182818284",
    "name": "Non-member"
  },
  "cc": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  }
}
```

❓ **Question:** Should other addressees be included in the `cc` property? For example, the admins, the owner, or the members?

❓ **Question:** Is it necessary to specify which actors can invite others to the group, or leave it up to the implementation?

To expel someone from a group ([Expel from a group][5]), an actor sends an `Remove` activity for the actor being expelled. The sending actor must have authorization to expel other actors.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/groups/world-group/admins/3456789012",
  "type": "Remove",
  "object": {
    "id": "https://example.com/actors/27182818284",
    "type": "Person",
    "name": "Removed member"
  },
  "target": {
    "type": "OrderedCollection",
    "id":  "https://example.com/groups/world-group/members",
    "name": "World Group members"
  },
  "to": [
    {
      "type": "Group",
      "id": "https://example.com/groups/world-group",
      "name": "World Group"
    },
    {
      "id": "https://example.com/actors/27182818284",
      "type": "Person",
      "name": "Removed member"
    }
  ]
}
```

🚪 **Alternative** Other options exist for removing a member, such as using a `Reject` with their original `Join` activity, or using a `Block` activity.

❓ **Question:** Who has authorization to expel a member? The owner, the admins, members? Protocol-defined, or implementation dependent?

### Group lifecycle

The lifecycle of a group object -- creation, update, and deletion -- is similar to the lifecycle of other ActivityPub objects. The group object is created, updated, and deleted using the same activities as other objects.

To create a group ([Create a group][3]), an actor sends a `Create` activity with the group as the `object` property. As with other `Create` activities, the addressing of the activity is the authorization list for visibility for the created object.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Create",
  "object": {
    "type": "Group",
    "name": "World Group"
  },
  "to": "as:Public"
}
```

❓ **Question:** This will create a group on the server of the actor. Dedicated group servers may use other methods to create a group. One option is to log in to the group server as an API client to the user's account server, and then post a `Create` activity for the group with the `id` already set, to indicate that the creation is already complete.

To read a group's information ([Get group info][21]), an actor fetches the group object using an HTTP GET request to the object `id` property. This will return a JSON-LD document with the group information, such as the object shown in "Group representation" above.

To update a group ([Change group info][22]), an actor sends an `Update` activity with the group as the `object` property. The activity must include the `object` property, which is the group to update.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Update",
  "object": {
    "id": "https://example.com/groups/world-group",
    "summary": "This is a new group description."
  },
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  }
}
```

❓ **Question:** Again, the user's account server and the `Group` server may be different. Is this properly handled by this configuration?

To delete a group ([Close a group][16]), an actor sends a `Delete` activity with the group as the `object` property. The activity must include the `object` property, which is the group to delete.

```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "id": "https://example.com/activities/1234567890",
  "actor": "https://example.com/actors/3456789012",
  "type": "Delete",
  "object": {
    "id": "https://example.com/groups/world-group"
  },
  "to": {
    "type": "Group",
    "id": "https://example.com/groups/world-group",
    "name": "World Group"
  }
}
```

❓ **Question:** Does the `Delete` activity need to have any boundaries, or should this be left up to implementations?

### Collections

TBD

### Admins

TBD

## Alternative designs

TBD

## Open issues

TBD

### Assumed structure

TBD

### Group as actor

TBD

### Owner

TBD

[swicg]: https://www.w3.org/community/socialweb/
[issues]: https://github.com/swicg/groups/issues
[user story issue tag]: https://github.com/swicg/groups/issues?q=label%3A%22user%20story%22%20
[1]:  https://github.com/swicg/groups/issues/1
[2]: https://github.com/swicg/groups/issues/2
[3]: https://github.com/swicg/groups/issues/3
[4]: https://github.com/swicg/groups/issues/4
[5]: https://github.com/swicg/groups/issues/5
[6]: https://github.com/swicg/groups/issues/6
[7]: https://github.com/swicg/groups/issues/7
[8]: https://github.com/swicg/groups/issues/8
[9]: https://github.com/swicg/groups/issues/9
[10]: https://github.com/swicg/groups/issues/10
[11]: https://github.com/swicg/groups/issues/11
[12]: https://github.com/swicg/groups/issues/12
[13]: https://github.com/swicg/groups/issues/13
[14]: https://github.com/swicg/groups/issues/14
[16]: https://github.com/swicg/groups/issues/16
[18]: https://github.com/swicg/groups/issues/18
[19]: https://github.com/swicg/groups/issues/19
[20]: https://github.com/swicg/groups/issues/20
[21]: https://github.com/swicg/groups/issues/21
[22]: https://github.com/swicg/groups/issues/22