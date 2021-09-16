# Steps to take after a Merge Request is reviewed

These steps must be taken after your merge request was reviewed and some changes were requested.

## Addressing each change

1. Understand the suggested review change. Ask questions if not clear.
2. Make the necessary change.
3. If the suggested code is too big and time taking, discuss.
4. After the code change was addressed, leave comment in the thread (GitLab).
5. Make sure you address any other instance of a particular review comment throughout the MR. For example, if you 
   were asked to remove print statements at one line, you check for other places in that MR.

## Testing the changes

1. You must perform all the tests that you mentioned in the initial MR - [Descriptions](after-merge-request.md#description).
2. Add any other test coverage point you covered.

## Pushing the changes

1. Add a good commit description and push your changes. Examples-
   1. `refactor: Update the logic of user login COOEE-123`,
   2. `fix: Add missing file in Git COOEE-124`
   3. `refactor: Do multiple review changes in user login feature COOEE-123`
2. Resolve each & individual thread in GitLab which was addressed.
3. Perform all the necessary steps mentioned in the [after-merge-request.md](after-merge-request.md)