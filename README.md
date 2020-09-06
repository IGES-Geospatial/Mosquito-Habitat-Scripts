# Mosquito Habitat Mapper Notebooks

This repository contains three notebooks: User Improvement, Regional Analysis, and Data Cleaning used to download different subsets of data from the GLOBE Mosquito Habitat Mapper Protocol. User Improvement formats the data so it is easier to track user improvement, Regional Analysis facilitates the analysis of certain countries or GLOBE Regions, and Data Cleaning cleans data and can also download photos from the Mosquito Habitat Mapper Data.

## User Improvement
This Notebook is designed to facilitate the tracking of user improvement. It takes all mosquito habitat mapper observations and reorders them such that the users with the most observations appear first in the dataset with their entries from earliest to latest.

## Regional Analysis
This Notebook contains two scripts to facilitate the analysis of areas of interest: a Regional Separation Script and a Country Script. 

### Regional Separation Script
The Regional Separation script downloads data from a specific GLOBE region. Each region has a list of associated countries. The script iterates through the primary mosquito habitat mapper dataset and verifies if the country (countryName) is inside the desired region's country list. If it is, the script appends the entry to a dataset containing the entries for the desired region. 
### Country Script
Similarly, the Country script iterates through the mosquito mapper dataset, but it only appends the entry to a separate dataset if the country name precisely matches the desired country.

## Data Cleaning
This Notebook contains three scripts to facilitate the downloading and cleaning of data. Two cleaning scripts filter the data: the Geolocational Data script and the Possible Event script while the Photo Downloader fetches photos from the GLOBE Website. 

### Geolocational Data Script
The Geolocational Data script attempts to filter out any entries that contain inaccurate geographic measurements. The script iterates through mosquito mapper entries and verifies if it meets either one of two conditions. The first condition is if the site latitude and longitude (latitude, longitude) match the latitude and longitude measured by the GPS (mosquitohabitatMeasurementLatitude, mosquitohabitatMeasurementLongitude). The second condition is if the GPS latitude or longitude are integers. If an entry meets at least one of the two conditions, the script drops it from the dataset.

### Possible Event Script
The Possible Event script attempts to identify possible sets of entries in the dataset caused by mosquito habitat mapper training events. The script groups together entries that contain the same date (measuredDate), site latitude (latitude), site longitude (Longitude), water source (mosquitohabitatmapperWaterSource), and site name (siteName). The script filters these groups resulting in a list of groups that contain more than ten entries (note that this threshold is adjustable). It stores these "possible event" entries in one dataset and removes those entries from the primary dataset. These datasets become separate CSV files for further analysis.

### Photo Downloading Script
The last script, the Photo Downloading script downloads the photos from the possible event groups to help a human later identify which groups are training events and download all the photos from the clean dataset into a separate folder.

It takes the groups discovered by the Possible Event script and iterates through each Possible Event group. For every group, it creates a folder. Then, the Photo Downloading script goes through each entry of the group data and downloads the pictures contained in each entry. Finally, it generates two CSV files: one that lists all the images downloaded and one having all the mosquito mapper entries for that group. These files are used in conjunction with the pictures to verify that the identified group was a training event.

Then for the clean dataset, it goes through each entry and adds all the pictures to a folder. Once it's done, it generates a CSV with all the filenames, photo URLs, and attributions.



