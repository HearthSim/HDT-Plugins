# HDT plugin list

this repo is meant to keep a list of plugins for the (upcoming) HDT plugin browser.

## guidelines for repositories

these are general guidelines for repositories to be included on this list. Special exceptions can be made if the repository cannot be changed. 

  - Release tags must be in the formst of `vx.x` or `x.x`. They will be converted to Version objects at runtime and be compared to the versiom number supplied in your `IPlugin`.
  - The download should be a .dll or .zip file uploaded to the downloads section of the release. Will take the first download available in cases of 2 or more download files.
  - When updating it will install exactly like a manual install, so make sure the release download will not overwrite any config files.
  - if any of these conditions are not in proper order, it will instead directly link to the Latest release page.
  
  
Readme not finished
