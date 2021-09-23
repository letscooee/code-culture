# Steps to take after a Merge Request is reviewed

These steps must be taken after your merge request was reviewed and some changes were requested.

## 1. Addressing each change

1. Understand the suggested review change. Ask questions if not clear.
2. Make the necessary changes.
3. If the suggested code is too big and time taking, discuss.
4. Make sure you address any other instance of a particular review comment throughout the MR. For example, if you
      were asked to remove print statements at one line, you check for other places in that MR.
5. Add a good commit descriptions. For examples-
   1. `refactor: Update the logic of user login COOEE-123`,
   2. `fix: Add missing file in Git COOEE-124`
   3. `refactor: Do multiple review changes in user login feature COOEE-123`

## 2. Testing the changes

1. You must perform all the tests that you mentioned in the initial MR - [Testing performed](after-merge-request.md#testing-performed).
2. Add any other test coverage point you covered.

## 3. Pushing the changes & re-submit for review

1. After all the code changes were addressed, **push your changes in the same branch**.
   1. For trivial changes, you can amend your last commit and force push to your branch.
2. leave comment in the thread (GitLab).
3. Resolve each & individual thread in GitLab which was addressed **by leaving comment and resolving them**.
4. Perform all the steps again mentioned in the [after-merge-request.md](after-merge-request.md)