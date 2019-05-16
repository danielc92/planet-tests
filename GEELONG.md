# Collecting data for one of the areas of interest (Geelong)

1. Update the filter file to a new date range of 2018-2019. Update the coordinate box values.

2. Run command `python search_endpoint.py | jq '.features[].id'` in terminal

*Note: From the output it appears that the last images were collected in February 2019.*

Output:
```sh
"20190211_001638_5521506_RapidEye-4"
"20190211_001642_5521405_RapidEye-4"
"20190211_001642_5521406_RapidEye-4"
"20190124_000357_5521405_RapidEye-1"
"20190124_000353_5521506_RapidEye-1"
"20190124_000354_5521505_RapidEye-1"
"20190124_000356_5521406_RapidEye-1"
"20181126_001833_5521506_RapidEye-3"
"20181025_002808_5521506_RapidEye-4"
"20181025_002809_5521505_RapidEye-4"
"20181025_002812_5521406_RapidEye-4"
"20181025_002812_5521405_RapidEye-4"
"20181024_002527_5521405_RapidEye-3"
"20181013_002353_5521506_RapidEye-2"
"20181013_002353_5521505_RapidEye-2"
"20181013_002356_5521406_RapidEye-2"
"20181013_002357_5521405_RapidEye-2"
"20181012_002022_5521506_RapidEye-1"
"20181012_002022_5521505_RapidEye-1"
"20181012_002026_5521405_RapidEye-1"
"20181012_002025_5521406_RapidEye-1"
"20180920_001152_5521506_RapidEye-3"
"20180920_001155_5521406_RapidEye-3"
"20180920_001156_5521405_RapidEye-3"
"20180920_001152_5521505_RapidEye-3"
"20180905_002541_5521505_RapidEye-2"
"20180905_002544_5521405_RapidEye-2"
"20180902_001526_5521406_RapidEye-4"
"20180902_001527_5521405_RapidEye-4"
"20180902_001523_5521506_RapidEye-4"
"20180902_001523_5521505_RapidEye-4"
"20180814_001614_5521405_RapidEye-4"
"20180814_001611_5521505_RapidEye-4"
"20180802_002839_5521506_RapidEye-1"
"20180802_002839_5521505_RapidEye-1"
"20180802_002843_5521405_RapidEye-1"
"20180802_002842_5521406_RapidEye-1"
"20180731_002150_5521405_RapidEye-4"
"20180731_002147_5521506_RapidEye-4"
"20180731_002147_5521505_RapidEye-4"
"20180731_002150_5521406_RapidEye-4"
"20180729_002713_5521506_RapidEye-2"
"20180729_002713_5521505_RapidEye-2"
"20180729_002716_5521406_RapidEye-2"
"20180729_002716_5521405_RapidEye-2"
"20180625_003013_5521506_RapidEye-1"
"20180625_003013_5521505_RapidEye-1"
"20180625_003016_5521405_RapidEye-1"
"20180622_002032_5521505_RapidEye-3"
"20180622_002032_5521506_RapidEye-3"
"20180622_002036_5521405_RapidEye-3"
"20180622_002035_5521406_RapidEye-3"
"20180611_003553_5521406_RapidEye-1"
"20180611_003553_5521405_RapidEye-1"
"20180611_003550_5521505_RapidEye-1"
"20180611_003549_5521506_RapidEye-1"
"20180323_003606_5521506_RapidEye-2"
"20180323_003607_5521505_RapidEye-2"
"20180323_003610_5521406_RapidEye-2"
"20180323_003610_5521405_RapidEye-2"
"20180304_003632_5521405_RapidEye-2"
"20180304_003628_5521506_RapidEye-2"
"20180304_003628_5521505_RapidEye-2"
"20180304_003631_5521406_RapidEye-2"
"20180301_002545_5521405_RapidEye-4"
```

3. Check asset keys using the following command in terminal 
```sh
curl -L -H "Authorization: api-key $PLANET_API_KEY" \
    'https://api.planet.com/data/v1/item-types/REOrthoTile/items/20190211_001638_5521506_RapidEye-4/assets' \
    | jq 'keys'
```

Output 
```sh
[
  "analytic",
  "analytic_xml",
  "udm",
  "visual",
  "visual_xml"
]
```

4. Check status of "visual" asset type
```sh
curl -L -H "Authorization: api-key $PLANET_API_KEY" \
    'https://api.planet.com/data/v1/item-types/REOrthoTile/items/20190211_001638_5521506_RapidEye-4/assets/' \
    | jq .visual.status

```

Output:
```sh
"inactive"
```

The output is inactive so we will have to activate it before we're allowed to download.

5. Activate
```sh
python activation.py
```

Output:
```sh
429
```

Something went wrong. Error code 429. (Too many requests)