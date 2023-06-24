# homepage_config
 Personal collection of config files for Homepage
 https://github.com/benphelps/homepage/
 
 Also included is `customtheme.css` showing how to further customize the colours.
 The easiest methods of using is likely either via a subfilter module in Nxinx (or similar), or a browser extenstion such as Stylus.
 
 Ex.
 ```
        proxy_set_header Accept-Encoding "";
        sub_filter
        '</head>'
        '<link rel="stylesheet" type="text/css" href="https://raw.githubusercontent.com/MountainGod2/homepage_config/main/customtheme.css">
        </head>';
        sub_filter_once on;
```

 or 

 ![homepage_stylus](https://github.com/MountainGod2/homepage_config/assets/88257202/531d0bc7-f6d4-4045-8f01-f3db13a4f874)


 # Screenshots

![homepage_dracula](https://github.com/MountainGod2/homepage_config/assets/88257202/d0157ecf-f4c7-4a57-aa8c-762b41e08591)


![homepage_ibracorp](https://github.com/MountainGod2/homepage_config/assets/88257202/4abcea11-22e8-46e0-bc33-56e6bec8af21)
