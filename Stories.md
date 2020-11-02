# Understanding Presalytics Stories

Once you get going with Presalytics, your starting point is most often a "Story".  With Presalytics, a story serves many functions with the application. 

We chose the term "Story" for the primary object in the Presalytics API.  We believe that within an organization, data analytics do not exist for their own stake, but rather analytics are most ofter needed to support a narrative.  Most data analysts spend their time cultivating analysis in order to influence a target audience, most ofter executives and customers. Our empahasis on creating "Stories", reflects our belief that analytics should provide insight and influence the thinking of their audience.

In the context the Presalytics.io, the story is the root object of the application.  When using client applications, such as the [webapp](/story/), a Story is the object you will modify to change the output of your decks and enable your automation.  If using the API, the bulk on your call will be to an endpoint in the [Story API](https://presalytics.io/docs/api-specifications/story/).

### Story Properties

Every story has a few properties that users should be familiar with:

* `id`: The story fingerprint.  A unique identifier for a give story.  Needed to make API calls.

* `title`: The story's title.  A few describing the story to its audience

* `outline`: The story's "outline" is a set of instructions that tell Presalytics how to render your story.  This property is important and is covered in detail on a [separate page](/docs/story-outlines).

* `revision`: An integer that increments each time a Story's outline is updated.

* `outline_history`: A list outlines from previous revisions.

* `is_public`: To true/false flag indicating whether users can anonymously view your story over the internet. By default this is false.

* `collaborators`: A story's collaborators are other Presalytics.io users that have permission to interact with your story.  Permissions you can grant are as follows:

{:.table}
    | Permission | Description |
    | :--------: |-------------|
    | Viewer | Can view the story |
    | Promoter | Can view the story and share it with other Presalytics users |
    | Editor | All the permissions of the promoter, and can make changes to the Story object itself, including the Story's outline |
    | Owner | All of the permissions of an editor, with the additional ability to delete the Story |
    | Creator | Same as owner, but reserved for the user that initially created the story |


* `ooxml_documents`: This is a list of Office Open Xml documents (e.g., Microsoft Office, Google Slides) that are considered "subdocuments" of this story.  One story can read and render content from different subdocuments.  For exmaple, A story could rendered from multiple  `.pptx` files, each of which is maintained by a different user.  This simplifies version control for collaborative teams.  Support for other file types (e.g., `.xlsx`, `.docx`) is being added. 

* `conversation`:  A Story's conversation is a container for all of the user events that happen as users interact with story.  The Story's chat messages, clicks and notifications are all part of the story's conversation.  To learn more about story events and webhooks, go to the [events page](/docs/events).

