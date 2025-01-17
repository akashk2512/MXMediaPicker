# MXMediaPicker
[![](https://jitpack.io/v/ming-xi/MXMediaPicker.svg)](https://jitpack.io/#ming-xi/MXMediaPicker)

A media picker for Android (supports Android 11) with fully customizable UI~
### Try Demo
![demo.gif](app/demo.gif)

[demo.apk](app/demo.apk) 


## Installing

Step 1. Add it in your root build.gradle at the end of repositories:

    allprojects {
        repositories {
            ...
            maven { url 'https://jitpack.io' }
        }
    }
Step 2. Add the dependency

    dependencies {
        implementation 'com.github.ming-xi:MXMediaPicker:1.0.8'
    }



## Usage
- Initialize with application context:
```
MXMediaPicker.init(getApplicationContext());
MXMediaPicker picker = MXMediaPicker.getInstance();
```
- Set your own custom holders. (If not set, default holders will be used)
```
picker.setFolderHolder(folderHolder);
picker.setImageHolder(imageHolder);
picker.setVideoHolder(videoHolder);
```
- Ask user for `Manifest.permission.READ_EXTERNAL_STORAGE`, then:

- Setup PickerConfig:
```
PickerConfig pickerConfig = new PickerConfig();
pickerConfig.setFileType(MXMediaPicker.FILE_TYPE_VIDEO_AND_IMAGE);
pickerConfig.setAllowCamera(false);
pickerConfig.setFolderMode(MXMediaPicker.FOLDER_MODE_ONLY_PARENT);
pickerConfig.setMultiSelect(true);
pickerConfig.setMultiSelectMaxCount(9);
picker.setPickerConfig(pickerConfig);
```
- Finnaly, call:

```
picker.chooseImage(MainActivity.this, REQ_CODE);
```
- And receive results in:
```
@Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQ_CODE) {
            List<ResultItem> selectedItems = MXMediaPicker.getInstance().getSelectedItems(resultCode, data);
                if (selectedItems != null) {
                    for (ResultItem item : selectedItems) {
                        String uri = item.getUri();
                        String path = item.getPath();
                        //Please read data from uri. Path is only used to get file name and extension. 
                    }                                        
                }
            }
        }
    }
```


## Built With

* [Glide](https://github.com/bumptech/glide) - For default Image display



## Authors

* **Michael Xu**  - [ArchangelXu](https://github.com/ArchangelXu)

See also the list of [contributors](https://github.com/ming-xi/MXMediaPicker/contributors) who participated in this project.

## License

This project is licensed under the Anti 996 License - see the [LICENSE](LICENSE) file for details