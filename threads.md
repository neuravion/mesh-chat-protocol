# Threads

Each message payload will have a populated `id` field, uniquely identifying that message.

Future messages may reference that `id` by setting `replied_to_id`. It is up to the client to determine how to display threads, but it's recommended to only have one level of indentation.

It is highly recommended to set the `replied_to_id` to the `id` of the last message in the thread, so that newly connected network members may benefit from thread categorization.

If the message with `id` matching `replied_to_id` doesn't exist -- it's possible that the client that received the message-to-be-threaded was not online when the parent message was sent to network members. The message should be placed at the end of the message queue like a regular message, and all future replied to the thread will be under that message.
