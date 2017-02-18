# HDT plugin list

this repo is meant to keep a list of plugins for the (upcoming) HDT plugin browser.

## Adding plugins and format for the plugin file

To get your plugin listed you will need to follow this format in the main plugins file. Your repository must also follow the guidelines below.

The program deseralizes the json for each item in the data array. The url is an API url to the repo page. THe plugin creators can dictate what the title and short description of their plugins are.

```JSON
{
  "url": "https://api.github.com/repos/:owner/:repo",
  "title": "YOUR_TITLE",
  "short_description": "YOUR_DESC"
}
```
Example:
```JSON
{
  "url": "https://api.github.com/repos/HearthSim/Hearthstone-Collection-Tracker",
  "title": "YOUR_TITLE",
  "short_description": "YOUR_DESC"
}
```

Make a pull request by appending your repo to the file.

## guidelines for repositories

these are general guidelines for repositories to be included on this list. Special exceptions can be made if the repository cannot be changed. 

* Release tags must be in the formst of `vx.x` or `x.x`. They will be converted to Version objects at runtime and be compared to the versiom number supplied in your `IPlugin`.
* The download should be a .dll or .zip file uploaded to the downloads section of the release. Will take the first download available in cases of 2 or more download files.
* When updating it will install exactly like a manual install, so make sure the release download will not overwrite any config files.

## Specifics and how it works

May not be completely accurate as this feature is not finalized yet.

When a user goes to browse plugins, it will download the plugins.json file. It will do a foreach loop for each dict object in the data array. On each loop it will:

* create a list item
* make an API request to [url]. The title is [title]. The description is [short_description]. Modifies the list item to these specs.
* make a github API request to [url]/releases/latest and parse the json. The `Tag_name` will be stripped of the letter `v`. 
* the above resulting string will be parsed into a version identifier. If the user already has the specified plugin it will compare versions and if there is an update will specify the plugin as "update available".
* list item: current version will be tag_name. download link will download the `browser_download_url` of the first dictionary entry in the assets array. The right-click context menu will have a "view in browser" which opens to latest release and "view info" link which opens the readme of the repo.

Upon clicking download:

* download the download link as specified above to a temporary directory.
* extract it to its own folder in the plugins directory. Will be heavily similar to [current drag and drop functionality](https://github.com/HearthSim/Hearthstone-Deck-Tracker/blob/master/Hearthstone%20Deck%20Tracker/FlyoutControls/Options/Tracker/TrackerPlugins.xaml.cs#L68).
* prompt the user to download more or restart (probably can be improved in the future).
* go ahead and mark the plugin as downloaded/installed.

Readme not finished
