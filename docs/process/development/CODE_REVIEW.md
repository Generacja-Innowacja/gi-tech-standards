# Code review

We have a code review process that is mandatory for all pull requests. Here is short description how to do this right,
to minimize the time spent on code review and to make it as effective as possible. We're working as a volunteer team, so
we want to make sure that the code review process is as smooth as possible.

## When code review happens?

Code review happens when a **developer** has completed a feature or bug fix and is ready to merge their code into the
_main_ branch. Start thinking about creating a pull request (PR) if you have:

- completed your feature or bug fix,
- the code is working on your end,
- the code _looks_ okay,
- you have tested it manually (by looking at the result)
- you have written tests for it.

## Code review process

When conditions from above are fulfilled, you can proceed with the code review process. The process is as follows:

1. **Create a pull request**: When feature or bug fix is completed, **developer** creates a pull request (PR) in the
repository. To do this, visit GitHub page of your repository, navigate to the "Pull requests" tab, and click on the
green _"New pull request"_ button. Select the branch you want to merge into the `main` branch and the branch you want to
merge. Make sure to resolve all the conflicts before creating a pull request. Do not forget to fill these fields:
   - **Title**: The title of the PR should be descriptive and in present simple tense. For example,
     _"Implement calculation results cache"._
   - **Description**: Description of the PR is usually not needed at all. Add something in this section only if you feel
   that reviewer should see something or remember something while reviewing the code.
   - **Labels**: We do not use GitHub labels for pull requests.
   - **Assignee**: Assign yourself as the author of the PR.
2. **Assign reviewers**: **Developer** assigns at least one reviewer to your PR. The reviewer should be someone who is
familiar with the codebase and can provide constructive feedback: usually it is a tech lead or another developer from
your project.
3. **Update board and inform a team**: After assigning the reviewers, **developer** should write a message on discord
`*-back` channel, and move task to `Code review` column in GitHub Projects.
4. **Review the code**: The **reviewer** should review the code for readability, maintainability, and adherence to
coding standards. They should also test the code to ensure it works as expected.
5. **Provide feedback**: The **reviewer** should provide feedback on the code, including any suggestions for improvement
or changes that need to be made. We decided to use [conventional comments](https://conventionalcomments.org/) standard
for giving feedback.
6. **Make changes**: If the reviewer requests changes, make the necessary changes to the code and push them to the PR.
If **reviewer** starts a discussion, you can reply to the comment and ask for more details. Do not resolve the comment
that was created by **reviewer**. Conversation resolving is the responsibility of the **reviewer**.
7. **Approve the PR**: Once the **reviewer** is satisfied with the changes, they should approve the PR.
8. **Merge the PR**: Once the PR has been approved, **developer** merges it into the main branch. Please do not hesitate
to click it, approved but not merged PRs are causing delays in the development process.
9. **Delete the branch**: Once the PR has been merged, delete the branch to keep the repository clean. This is usually
done automatically on our repositories, but make sure that the branch was removed.
10. **Deploy the code**: Once the PR has been merged, check if there is a deployment pipeline set up for the repository.
If there is, the code will be automatically deployed to the production environment. If not, manually deploy the code to
the production environment, or ask tech leader to do this.
11. **Close the task in GH Projects**: Once the PR has been merged and the code has been deployed, **developer** closes
the task in GitHub Projects.

**Legend:**

- **developer** - the person responsible for the code
- **reviewer** - other developer or tech lead that will review the code
