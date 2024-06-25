# Tips and Tricks developing
My intention is to collect some of the tips and tricks I use/search for developing

## Swift

### Build and run on change

When developing server apps in nodejs, is common to have some command watch to build and run the server on any change, this is not possible on swift. But I found the solution using entr. 

Create some watch.sh file (or similar) and put this into the contents:
```sh
find . -name "*.swift" | entr -s "swift build"
```

I've got pending to improve it, as currently doesn't support change adding new files or deleting them. 