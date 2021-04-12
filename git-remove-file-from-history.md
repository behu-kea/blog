# Remove file from git history



If you fx have accidentally added a password, then you need to not only remove where the password is stored. You also need to remove the history if that file so others cannot find the password just by looking through the commits. 



Use this command to remove the history for that file: **Remember to backup your files if any thing goes wrong!**

```bash
git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch PATH_TO_FILE" HEAD
```



Example:

```bash
git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch src/main/java/com/example/demo/repositories/WishlistRepository.java" HEAD
```



Again remember to backup the file, since the history will be changed, so you dont really know what you will get here!!!





