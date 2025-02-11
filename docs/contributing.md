# How to Contribute

Everyone can contribute to Flax, and we value everyone's contributions. 
You can contribute in many more ways than just writing code. Answering questions
on our [Discussions page](https://github.com/google/flax/discussions), helping
each other, and improving our documentation are extremely valuable to our
ecosystem.

We also appreciate if you spread the word, for instance by starring our Github
repo, or referencing Flax in blog posts of projects that used it.

This project follows
[Google's Open Source Community Guidelines](https://opensource.google/conduct/).

## Ways to contribute

We welcome pull requests (PRs), in particular for those issues
[marked as PR-ready](https://github.com/google/flax/issues?q=is%3Aopen+is%3Aissue+label%3A%22Status%3A+pull+requests+welcome%22). For other proposals, we ask that you first open a Github Issue or
Github Discussion to discuss your planned contribution.

## Contributing code using Pull Requests

We do all of our development using git, so basic knowledge is assumed.

Follow these steps to contribute code:

### Create a Pull Request in your own branch

1. Fork the Flax repository by clicking the 'Fork' button on the
   [repository page](http://www.github.com/google/flax). This creates a copy
   of the Flax repository in your own account.

2. Install Python >=3.6 and `svn` for running the tests (see below).

3. (Optional) Create a virtual environment or a Docker container. See 
   [`dev/README.md`](https://github.com/google/flax/blob/main/dev/README.md)
   for details on how to setup a Docker Container. To setup a virtual environment,
   run the following:

   ```bash
   python3.6 -m virtualenv env
   . env/bin/activate
   ```
  
   This ensures all your dependencies are installed in this environment.

4. `pip install` your fork from source. This allows you to modify the code
   and immediately test it out:

   ```bash
   git clone https://github.com/YOUR_USERNAME/flax
   cd flax
   pip install ".[testing]"
   pip install -e .
   pip install -r docs/requirements.txt
   ```

5. Add the Google Flax repo (not your fork) as an upstream remote, so you can use it to sync your
   changes.

   ```bash
   git remote add upstream http://www.github.com/google/flax
   ```


6. Create a branch where you will develop from:

   ```bash
   git checkout -b name-of-change
   ```

7. Implement your changes using your favorite editor (we recommend
   [Visual Studio Code](https://code.visualstudio.com/)).

   Make sure the tests pass by running the following command from the top of
   the repository:

   ```bash
   ./tests/run_all_tests.sh
   ```

8. Once your change is done, create a commit as follows 
   ([how to write a commit message](https://chris.beams.io/posts/git-commit/)):

   ```bash
   git add file1.py file2.py ...
   git commit -m "Your commit message"
   ```

   Then sync your code with the main repo:

   ```bash
   git rebase upstream/main
   ```

9. Finally push your commit on your development branch and create a remote 
   branch in your fork that you can use to create a Pull Request from:

   ```bash
   git push --set-upstream origin name-of-change
   ```
   
   After running the command, you should see a Github link in your terminal output that you can click on to create a Pull Request.
   If you do not see this link in the terminal after doing a `git push`, go to the Github web UI; there should be a button there that lets you turn the commit into a Pull Request yourself.

10. Make sure your PR passes the 
   [PR checklist](https://github.com/google/flax/blob/main/.github/pull_request_template.md#checklist).
   If so, create a Pull Request from the Flax repository and send it for review.
   Consult [GitHub Help](https://help.github.com/articles/about-pull-requests/)
   for more information on using pull requests.

### Updating the Pull Request contents

Every Pull Request should ideally be limited to just one commit, so if you have multiple commits please squash them.

Assuming you now have only one commit in your Pull Request, and want to add changes requested during review:

1. Make the changes locally in your editor.
2. Run `git commit -a --amend`. This updates the commit contents and allows you to edit the commit message.
3. At this point, `git push` alone will result in an error. Instead, use `git push --force`.
4. Check that it's done: The changes to your commit should be immediately reflected in the Github web UI.

## Troubleshooting

### Too many commits in a PR

If your PR has too many commits associated with it, then our build process will
fail with an error message. This is because of two reasons:

* We prefer to keep our commit history clean.

* Our source sync process will fail if our commit tree is too large.

If you encounter this error message, you should squash your commits. In order to
rebase your branch to main and creating a new commit containing all your
changes, please run the following command:

```bash
git rebase main && git reset --soft main && git commit
```

This will apply all your changes to the main branch. Note that if you had to
resolve any conflicts while working on your change (for instance, you did a
`pull upstream main` which led to conflict), then you will have to resolve these
conflicts agin.

Once you successfully rebased your branch, you should push your changes. Since
you are changing the commit history, you should use `git push --force`.

## Contributor License Agreement

Contributions to this project must be accompanied by a Contributor License
Agreement. You (or your employer) retain the copyright to your contribution;
this simply gives us permission to use and redistribute your contributions as
part of the project. Head over to <https://cla.developers.google.com/> to see
your current agreements on file or to sign a new one.

You generally only need to submit a CLA once, so if you've already submitted one
(even if it was for a different project), you probably don't need to do it
again.
