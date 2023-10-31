If you want to move multiple commits from one branch to another without using `cherry-pick` or `rebase`, you can use the `git format-patch` and `git am` commands in combination with a range of commits. Here's how you can do it:

1. **Generate Patch Files for Multiple Commits**:

   ```bash
   git checkout <source_branch>
   git format-patch -o <output_directory> <start_commit>..<end_commit>
   ```

   Replace `<source_branch>` with the name of the branch containing the commits you want to move, `<output_directory>` with the directory where you want to save the patch files, `<start_commit>` with the hash of the first commit, and `<end_commit>` with the hash of the last commit in the range.

   This will generate patch files for each commit in the specified range.

2. **Switch to the Target Branch**:

   ```bash
   git checkout <target_branch>
   ```

   Replace `<target_branch>` with the name of the branch where you want to apply the changes.

3. **Apply the Patches**:

   ```bash
   git am <path_to_patch_directory>/*.patch
   ```

   Replace `<path_to_patch_directory>` with the actual path to the directory containing the generated patch files.

4. **Resolve Conflicts (if any)**:

   If there are any conflicts during the `git am` process, you'll need to resolve them. Git will guide you through the process.

5. **Commit the Changes (if needed)**:

   If there were no conflicts or after you've resolved them, you'll need to commit the changes:

   ```bash
   git commit -m "Message"
   ```

6. **Clean Up (optional)**:

   If you want to remove the commits from the original branch, you can use:

   ```bash
   git checkout <original_branch>
   git reset --hard <start_commit>^..HEAD
   ```

   Replace `<original_branch>` with the name of the original branch and `<start_commit>` with the hash of the first commit in the range.

   Be cautious with this step, as it permanently removes the selected commits from the original branch's history.

7. **Push the Changes**:

   ```bash
   git push origin <target_branch>
   ```

Now, the specified range of commits has been moved from the original branch to the target branch using the patch-based method.
