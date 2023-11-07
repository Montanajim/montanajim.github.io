# Read JSON From Webpage





## Key Points



### Future Builder

In Flutter, a `FutureBuilder` widget is used to manage the asynchronous nature of data fetching and display. It takes a `future` object, which represents an asynchronous operation, and builds a widget based on the current state of the future. The `snapshot` parameter of the `builder` callback function provides information about the current state of the future.

The `snapshot` object has three main properties:

1. **`ConnectionState`**: This property indicates the current state of the future. It can be one of three values: `ConnectionState.none`, `ConnectionState.waiting`, or `ConnectionState.done`.
1. **`hasData`**: This property is `true` if the future has completed successfully and contains data, and `false` otherwise.
1. **`data`**: This property holds the data that was returned by the future, if the future has completed successfully. If the future has not completed, or if it completed with an error, then `data` is `null`.

The `builder` callback function is responsible for building the widget that will be displayed based on the current state of the future. It is important to handle all possible states of the future, including when the future is still waiting for data, when the future has completed successfully with data, and when the future has completed with an error. (AIBRDJG)



###  jsonDecode


In Dart, `jsonDecode` is a function used to parse a JSON string and convert it into a Dart object. It is a member of the `dart:convert` library, which provides a variety of functions for working with JSON data.

The `jsonDecode` function takes a single argument, which is the JSON string to be parsed. It returns the corresponding Dart object, which can be a Map, List, String, int, double, bool, or null. (AIBRDJG)

### HTTP Response

An HTTP response from a POST command consists of several parts, each of which plays a crucial role in conveying information about the request and its outcome. These parts include:

**Status Line:** The status line is the first line of the response and provides an initial indication of the request's success or failure. It consists of three components:

1.  **HTTP Version:** This indicates the version of the HTTP protocol used in the response.
1.  **Status Code:** This is a three-digit number that indicates the outcome of the request. Common status codes include 200 (OK), 400 (Bad Request), and 500 (Internal Server Error). 
1. **Status Phrase:** This is a brief description of the status code, providing additional context about the response.

**Headers:** Headers are a collection of key-value pairs that provide additional information about the response, such as the content type, content length, and caching instructions. Headers are essential for understanding how to handle the response content.

**Message Body (Optional):** The message body, if present, contains the actual data that was requested or submitted in the POST command. The content type header specifies the format of the message body, such as JSON, text, or an image.

**Response Trailer (Optional):** Response trailers are an optional set of key-value pairs that are appended to the end of the message body. They provide additional information about the response, similar to headers, but are only sent after the entire message body has been transmitted.

Here's an example of a complete HTTP response from a POST command:  Note that **Content-Type** is defining what is the **body**.

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123
Cache-Control: no-cache

{
  "message": "The request was successful.",
  "data": {
    "name": "John Doe",
    "age": 30
  }
}
```

In this example, the status line indicates that the request was successful (200 OK). The headers provide information about the content type (JSON), content length (123 bytes), and caching instructions (no caching). The message body contains the response data in JSON format, including a message and associated data. (AIBRDJG)

---



```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Flutter Auto Sales',
        debugShowCheckedModeBanner: false,
        theme: ThemeData(primarySwatch: Colors.red),
        home: const MyHomePage());
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  MyHomePageState createState() => MyHomePageState();
}

class MyHomePageState extends State<MyHomePage> {
  // ignore: prefer_typing_uninitialized_variables
  static dynamic data;

  // run on start

  static Future getData() async {
      
    var url = Uri.parse("https://flutter.locusnoesis.com/carinfo.php");

    http.Response response = await http.post(url);

    data = await jsonDecode(response.body);

    return data;
  }

  // Note that the FutureBuilder returns a Widget.
  // Note that the data return
  // in the object
  Widget myWidget = FutureBuilder(
      future: getData(),
      builder: (BuildContext context, AsyncSnapshot snapshot) {
        if (snapshot.hasData) {
          return ListView.builder(
            itemCount: data.length,
            itemBuilder: (BuildContext context, int index) {
              return Card(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  mainAxisSize: MainAxisSize.min,
                  children: [
                    ListTile(
                      title:
                          Text("${data[index]['year']} ${data[index]['make']}"),
                      subtitle: Text(
                          "${data[index]['model']} | ${data[index]['body_styles']}"),
                    )
                  ],
                ),
              );
            },
          );
        }
        return const Text("Getting Data");
      });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Flutters Cars"),
        centerTitle: true,
      ),
      body: Column(
        children: [
          Container(
              alignment: Alignment.centerLeft,
              padding: const EdgeInsets.all(20),
              child: Text(
                "Cars For Sale",
                style: TextStyle(
                    color: Colors.indigo[800],
                    fontWeight: FontWeight.bold,
                    fontSize: 18.0),
                textAlign: TextAlign.left,
              )),
          Expanded(child: myWidget)
        ],
      ),
    );
  }
}

```



## PHP Code for Webpage

```php
<?php
  $host_name =	'**********';
  $database = 	'**********';
  $user_name = 	'**********';
  $password = 	'**********';
  $dbh = null;

  try {
    $dbh = new PDO("mysql:host=$host_name; dbname=$database;", $user_name, $password);
  } catch (PDOException $e) {
    echo "Error!: " . $e->getMessage() . "<br/>";
    die();
  }
  
  
  
  
$query = 'SELECT * FROM tbl_cars';
$stm = $dbh->prepare($query);
$stm->execute();
$row = $stm->fetchAll(PDO::FETCH_ASSOC);
echo json_encode($row);
  
?>
```

## pubspec.yaml

```yaml
name: flutter_readjson_webpage
description: A new Flutter project.
# The following line prevents the package from being accidentally published to
# pub.dev using `flutter pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev

# The following defines the version and build number for your application.
# A version number is three numbers separated by dots, like 1.2.43
# followed by an optional build number separated by a +.
# Both the version and the builder number may be overridden in flutter
# build by specifying --build-name and --build-number, respectively.
# In Android, build-name is used as versionName while build-number used as versionCode.
# Read more about Android versioning at https://developer.android.com/studio/publish/versioning
# In iOS, build-name is used as CFBundleShortVersionString while build-number is used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
# In Windows, build-name is used as the major, minor, and patch parts
# of the product and file versions while build-number is used as the build suffix.
version: 1.0.0+1

environment:
  sdk: '>=3.0.5 <4.0.0'

# Dependencies specify other packages that your package needs in order to work.
# To automatically upgrade your package dependencies to the latest versions
# consider running `flutter pub upgrade --major-versions`. Alternatively,
# dependencies can be manually updated by changing the version numbers below to
# the latest version available on pub.dev. To see which dependencies have newer
# versions available, run `flutter pub outdated`.
dependencies:
  flutter:
    sdk: flutter
    
  # ***************** THIS IS ADDED ******************************
  # **************************************************************
  http: ^1.1.0
  # **************************************************************
  # **************************************************************


  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter

  # The "flutter_lints" package below contains a set of recommended lints to
  # encourage good coding practices. The lint set provided by the package is
  # activated in the `analysis_options.yaml` file located at the root of your
  # package. See that file for information about deactivating specific lint
  # rules and activating additional ones.
  flutter_lints: ^2.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter packages.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  # assets:
  #   - images/a_dot_burr.jpeg
  #   - images/a_dot_ham.jpeg

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/assets-and-images/#resolution-aware

  # For details regarding adding assets from package dependencies, see
  # https://flutter.dev/assets-and-images/#from-packages

  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  # fonts:
  #   - family: Schyler
  #     fonts:
  #       - asset: fonts/Schyler-Regular.ttf
  #       - asset: fonts/Schyler-Italic.ttf
  #         style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/custom-fonts/#from-packages

```



## SQL File

```sql
-- phpMyAdmin SQL Dump
-- version 4.9.11
-- https://www.phpmyadmin.net/
--
-- Host: db734633192.db.1and1.com
-- Generation Time: Nov 01, 2023 at 08:46 PM
-- Server version: 5.7.42-log
-- PHP Version: 7.0.33-0+deb9u12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET AUTOCOMMIT = 0;
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `db734633192`
--

-- --------------------------------------------------------

--
-- Table structure for table `tbl_cars`
--

CREATE TABLE `tbl_cars` (
  `year` int(4) DEFAULT NULL,
  `make` varchar(13) DEFAULT NULL,
  `model` varchar(31) DEFAULT NULL,
  `body_styles` varchar(35) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

--
-- Dumping data for table `tbl_cars`
--

INSERT INTO `tbl_cars` (`year`, `make`, `model`, `body_styles`) VALUES
(2022, 'Acura', 'ILX', 'Sedan'),
(2022, 'Acura', 'MDX', 'SUV'),
(2022, 'Acura', 'RDX', 'SUV'),
(2022, 'Acura', 'TLX', 'Sedan'),
(2022, 'Alfa Romeo', 'Giulia', 'Sedan'),
(2022, 'Alfa Romeo', 'Stelvio', 'SUV'),
(2022, 'Audi', 'A3', 'Sedan'),
(2022, 'Audi', 'A4', 'Sedan'),
(2022, 'Audi', 'A4 allroad', 'Wagon'),
(2022, 'Audi', 'A5', 'Coupe'),
(2022, 'Audi', 'A6', 'Sedan'),
(2022, 'Audi', 'A6 allroad', 'Wagon'),
(2022, 'Audi', 'A7', 'Sedan'),
(2022, 'Audi', 'e-tron', 'SUV'),
(2022, 'Audi', 'e-tron GT', 'Sedan'),
(2022, 'Audi', 'Q3', 'SUV'),
(2022, 'Audi', 'Q4 e-tron', 'SUV'),
(2022, 'Audi', 'Q5', 'SUV'),
(2022, 'Audi', 'Q7', 'SUV'),
(2022, 'Audi', 'Q8', 'SUV'),
(2022, 'Audi', 'R8', 'Coupe'),
(2022, 'Audi', 'S5', 'Convertible & Sedan & Coupe'),
(2022, 'Audi', 'SQ5', 'SUV'),
(2022, 'Audi', 'SQ5 Sportback', 'SUV'),
(2022, 'Audi', 'TT', 'Coupe'),
(2022, 'BMW', '2 Series', 'Sedan'),
(2022, 'BMW', '3 Series', 'Sedan'),
(2022, 'BMW', '4 Series', 'Coupe & Convertible'),
(2022, 'BMW', '5 Series', 'Sedan'),
(2022, 'BMW', '7 Series', 'Sedan'),
(2022, 'BMW', '8 Series', 'Sedan & Coupe & Convertible'),
(2022, 'BMW', 'i4', 'Coupe'),
(2022, 'BMW', 'iX', 'SUV'),
(2022, 'BMW', 'M3', 'Sedan'),
(2022, 'BMW', 'M4', 'Coupe'),
(2022, 'BMW', 'M5', 'Sedan'),
(2022, 'BMW', 'M8', 'Hatchback & Coupe & Convertible'),
(2022, 'BMW', 'X1', 'SUV'),
(2022, 'BMW', 'X2', 'SUV'),
(2022, 'BMW', 'X3', 'SUV'),
(2022, 'BMW', 'X4', 'SUV'),
(2022, 'BMW', 'X5', 'SUV'),
(2022, 'BMW', 'X6', 'SUV'),
(2022, 'BMW', 'X7', 'SUV'),
(2022, 'BMW', 'Z4', 'Convertible'),
(2022, 'Buick', 'Enclave', 'SUV'),
(2022, 'Buick', 'Encore', 'SUV'),
(2022, 'Buick', 'Encore GX', 'SUV'),
(2022, 'Buick', 'Envision', 'SUV'),
(2022, 'Cadillac', 'CT4', 'Sedan'),
(2022, 'Cadillac', 'CT5', 'Sedan'),
(2022, 'Cadillac', 'Escalade', 'SUV'),
(2022, 'Cadillac', 'Escalade ESV', 'SUV'),
(2022, 'Cadillac', 'XT4', 'SUV'),
(2022, 'Cadillac', 'XT5', 'SUV'),
(2022, 'Cadillac', 'XT6', 'SUV'),
(2022, 'Chevrolet', 'Blazer', 'SUV'),
(2022, 'Chevrolet', 'Bolt EUV', 'Hatchback'),
(2022, 'Chevrolet', 'Bolt EV', 'Hatchback'),
(2022, 'Chevrolet', 'Camaro', 'Coupe & Convertible'),
(2022, 'Chevrolet', 'Colorado Crew Cab', 'Pickup'),
(2022, 'Chevrolet', 'Colorado Extended Cab', 'Pickup'),
(2022, 'Chevrolet', 'Corvette', 'Coupe & Convertible'),
(2022, 'Chevrolet', 'Equinox', 'SUV'),
(2022, 'Chevrolet', 'Express 2500 Cargo', 'Van/Minivan'),
(2022, 'Chevrolet', 'Malibu', 'Sedan'),
(2022, 'Chevrolet', 'Silverado 1500 Double Cab', 'Pickup'),
(2022, 'Chevrolet', 'Silverado 1500 Limited Crew Cab', 'Pickup'),
(2022, 'Chevrolet', 'Silverado 2500 HD Double Cab', 'Pickup'),
(2022, 'Chevrolet', 'Spark', 'Hatchback'),
(2022, 'Chevrolet', 'Suburban', 'SUV'),
(2022, 'Chevrolet', 'Tahoe', 'SUV'),
(2022, 'Chevrolet', 'Trailblazer', 'SUV'),
(2022, 'Chevrolet', 'Traverse', 'SUV'),
(2022, 'Chevrolet', 'Trax', 'SUV'),
(2022, 'Chrysler', '300', 'Sedan'),
(2022, 'Chrysler', 'Pacifica', 'Van/Minivan'),
(2022, 'Chrysler', 'Pacifica Hybrid', 'Van/Minivan'),
(2022, 'Dodge', 'Challenger', 'Coupe'),
(2022, 'Dodge', 'Charger', 'Sedan'),
(2022, 'Dodge', 'Durango', 'SUV'),
(2022, 'FIAT', '500X', 'SUV'),
(2022, 'Ford', 'Bronco', 'SUV'),
(2022, 'Ford', 'Bronco Sport', 'SUV'),
(2022, 'Ford', 'EcoSport', 'SUV'),
(2022, 'Ford', 'Edge', 'SUV'),
(2022, 'Ford', 'Escape', 'SUV'),
(2022, 'Ford', 'Expedition', 'SUV'),
(2022, 'Ford', 'Explorer', 'SUV'),
(2022, 'Ford', 'F150 Lightning', 'Pickup'),
(2022, 'Ford', 'F150 SuperCrew Cab', 'Pickup'),
(2022, 'Ford', 'F250 Super Duty Crew Cab', 'Pickup'),
(2022, 'Ford', 'F250 Super Duty Regular Cab', 'Pickup'),
(2022, 'Ford', 'F250 Super Duty Super Cab', 'Pickup'),
(2022, 'Ford', 'F350 Super Duty Crew Cab', 'Pickup'),
(2022, 'Ford', 'F450 Super Duty Crew Cab', 'Pickup'),
(2022, 'Ford', 'Maverick', 'Pickup'),
(2022, 'Ford', 'Mustang', 'Coupe'),
(2022, 'Ford', 'Mustang MACH-E', 'SUV'),
(2022, 'Ford', 'Ranger SuperCrew', 'Pickup'),
(2022, 'Ford', 'Transit 250 Cargo Van', 'Van/Minivan'),
(2022, 'Ford', 'Transit Connect Cargo Van', 'Van/Minivan'),
(2022, 'Ford', 'Transit Connect Passenger Wagon', 'Van/Minivan'),
(2022, 'Genesis', 'Electrified G80', 'Sedan'),
(2022, 'Genesis', 'G70', 'Sedan'),
(2022, 'Genesis', 'G80', 'Sedan'),
(2022, 'Genesis', 'G90', 'Sedan'),
(2022, 'Genesis', 'GV60', 'SUV'),
(2022, 'Genesis', 'GV70', 'SUV'),
(2022, 'Genesis', 'GV80', 'SUV'),
(2022, 'GMC', 'Acadia', 'SUV'),
(2022, 'GMC', 'Canyon Crew Cab', 'Pickup'),
(2022, 'GMC', 'Canyon Extended Cab', 'Pickup'),
(2022, 'GMC', 'Hummer EV', 'Pickup'),
(2022, 'GMC', 'Savana 2500 Cargo', 'Van/Minivan'),
(2022, 'GMC', 'Sierra 1500 Double Cab', 'Pickup'),
(2022, 'GMC', 'Sierra 1500 Limited Crew Cab', 'Pickup'),
(2022, 'GMC', 'Sierra 2500 HD Crew Cab', 'Pickup'),
(2022, 'GMC', 'Sierra 2500 HD Double Cab', 'Pickup'),
(2022, 'GMC', 'Sierra 2500 HD Regular Cab', 'Pickup'),
(2022, 'GMC', 'Terrain', 'SUV'),
(2022, 'GMC', 'Yukon', 'SUV'),
(2022, 'GMC', 'Yukon XL', 'SUV'),
(2022, 'Honda', 'Accord', 'Sedan'),
(2022, 'Honda', 'Accord Hybrid', 'Sedan'),
(2022, 'Honda', 'Civic', 'Sedan & Hatchback'),
(2022, 'Honda', 'Civic Type R', 'Hatchback'),
(2022, 'Honda', 'CR-V', 'SUV'),
(2022, 'Honda', 'CR-V Hybrid', 'SUV'),
(2022, 'Honda', 'HR-V', 'SUV'),
(2022, 'Honda', 'Insight', 'Sedan'),
(2022, 'Honda', 'Odyssey', 'Van/Minivan'),
(2022, 'Honda', 'Passport', 'SUV'),
(2022, 'Honda', 'Pilot', 'SUV'),
(2022, 'Honda', 'Ridgeline', 'Pickup'),
(2022, 'Hyundai', 'Accent', 'Sedan'),
(2022, 'Hyundai', 'Elantra', 'Sedan'),
(2022, 'Hyundai', 'Ioniq 5', 'SUV'),
(2022, 'Hyundai', 'Ioniq Hybrid', 'Hatchback'),
(2022, 'Hyundai', 'Ioniq Plug-in Hybrid', 'Hatchback'),
(2022, 'Hyundai', 'Kona', 'SUV'),
(2022, 'Hyundai', 'Kona Electric', 'SUV'),
(2022, 'Hyundai', 'NEXO', 'SUV'),
(2022, 'Hyundai', 'Palisade', 'SUV'),
(2022, 'Hyundai', 'Santa Cruz', 'Pickup'),
(2022, 'Hyundai', 'Santa Fe', 'SUV'),
(2022, 'Hyundai', 'Santa Fe Hybrid', 'SUV'),
(2022, 'Hyundai', 'Santa Fe Plug-in Hybrid', 'SUV'),
(2022, 'Hyundai', 'Sonata', 'Sedan'),
(2022, 'Hyundai', 'Sonata Hybrid', 'Sedan'),
(2022, 'Hyundai', 'Tucson', 'SUV'),
(2022, 'Hyundai', 'Tucson Hybrid', 'SUV'),
(2022, 'Hyundai', 'Tucson Plug-in Hybrid', 'SUV'),
(2022, 'Hyundai', 'Veloster', 'Coupe'),
(2022, 'Hyundai', 'Venue', 'SUV'),
(2022, 'INFINITI', 'Q50', 'Sedan'),
(2022, 'INFINITI', 'Q60', 'Coupe'),
(2022, 'INFINITI', 'QX50', 'SUV'),
(2022, 'INFINITI', 'QX55', 'SUV'),
(2022, 'INFINITI', 'QX60', 'SUV'),
(2022, 'INFINITI', 'QX80', 'SUV'),
(2022, 'Jaguar', 'E-PACE', 'SUV'),
(2022, 'Jaguar', 'F-PACE', 'SUV'),
(2022, 'Jaguar', 'F-TYPE', 'Coupe & Convertible'),
(2022, 'Jaguar', 'I-PACE', 'SUV'),
(2022, 'Jeep', 'Cherokee', 'SUV'),
(2022, 'Jeep', 'Compass', 'SUV'),
(2022, 'Jeep', 'Gladiator', 'Pickup'),
(2022, 'Jeep', 'Grand Cherokee', 'SUV'),
(2022, 'Jeep', 'Grand Cherokee L', 'SUV'),
(2022, 'Jeep', 'Grand Wagoneer', 'SUV'),
(2022, 'Jeep', 'Renegade', 'SUV'),
(2022, 'Jeep', 'Wagoneer', 'SUV'),
(2022, 'Jeep', 'Wrangler', 'SUV'),
(2022, 'Jeep', 'Wrangler Unlimited', 'SUV'),
(2022, 'Jeep', 'Wrangler Unlimited 4xe', 'SUV'),
(2022, 'Kia', 'Carnival', 'Van/Minivan'),
(2022, 'Kia', 'EV6', 'SUV'),
(2022, 'Kia', 'Forte', 'Sedan'),
(2022, 'Kia', 'K5', 'Sedan'),
(2022, 'Kia', 'Niro', 'Wagon'),
(2022, 'Kia', 'Niro EV', 'Wagon'),
(2022, 'Kia', 'Niro Plug-in Hybrid', 'Wagon'),
(2022, 'Kia', 'Rio', 'Sedan'),
(2022, 'Kia', 'Seltos', 'SUV'),
(2022, 'Kia', 'Sorento', 'SUV'),
(2022, 'Kia', 'Sorento Hybrid', 'SUV'),
(2022, 'Kia', 'Sorento Plug-in Hybrid', 'SUV'),
(2022, 'Kia', 'Soul', 'Wagon'),
(2022, 'Kia', 'Sportage', 'SUV'),
(2022, 'Kia', 'Stinger', 'Sedan'),
(2022, 'Kia', 'Telluride', 'SUV'),
(2022, 'Land Rover', 'Defender 110', 'SUV'),
(2022, 'Land Rover', 'Defender 90', 'SUV'),
(2022, 'Land Rover', 'Discovery', 'SUV'),
(2022, 'Land Rover', 'Discovery Sport', 'SUV'),
(2022, 'Land Rover', 'Range Rover', 'SUV'),
(2022, 'Land Rover', 'Range Rover Evoque', 'SUV'),
(2022, 'Land Rover', 'Range Rover Sport', 'SUV'),
(2022, 'Land Rover', 'Range Rover Velar', 'SUV'),
(2022, 'Lexus', 'ES', 'Sedan'),
(2022, 'Lexus', 'GX', 'SUV'),
(2022, 'Lexus', 'IS', 'Sedan'),
(2022, 'Lexus', 'LC', 'Coupe'),
(2022, 'Lexus', 'LS', 'Sedan'),
(2022, 'Lexus', 'LX', 'SUV'),
(2022, 'Lexus', 'NX', 'SUV'),
(2022, 'Lexus', 'RC', 'Coupe'),
(2022, 'Lexus', 'RX', 'SUV'),
(2022, 'Lexus', 'UX', 'SUV'),
(2022, 'Lincoln', 'Aviator', 'SUV'),
(2022, 'Lincoln', 'Corsair', 'SUV'),
(2022, 'Lincoln', 'Nautilus', 'SUV'),
(2022, 'Lincoln', 'Navigator', 'SUV'),
(2022, 'Maserati', 'Ghibli', 'Sedan'),
(2022, 'Maserati', 'Levante', 'SUV'),
(2022, 'Maserati', 'Quattroporte', 'Sedan'),
(2022, 'MAZDA', 'CX-30', 'SUV'),
(2022, 'MAZDA', 'CX-5', 'SUV'),
(2022, 'MAZDA', 'CX-9', '[nil]'),
(2022, 'MAZDA', 'MAZDA3', 'Sedan'),
(2022, 'MAZDA', 'MX-30', 'SUV'),
(2022, 'MAZDA', 'MX-5 Miata', 'Convertible'),
(2022, 'Mercedes-Benz', 'A-Class', 'Sedan'),
(2022, 'Mercedes-Benz', 'C-Class', 'Coupe'),
(2022, 'Mercedes-Benz', 'CLA', 'Sedan'),
(2022, 'Mercedes-Benz', 'CLS', 'Sedan'),
(2022, 'Mercedes-Benz', 'E-Class', 'Sedan'),
(2022, 'Mercedes-Benz', 'G-Class', 'SUV'),
(2022, 'Mercedes-Benz', 'GLA', 'SUV'),
(2022, 'Mercedes-Benz', 'GLB', 'SUV'),
(2022, 'Mercedes-Benz', 'GLC', 'SUV'),
(2022, 'Mercedes-Benz', 'GLC Coupe', 'SUV'),
(2022, 'Mercedes-Benz', 'GLE', 'SUV'),
(2022, 'Mercedes-Benz', 'GLS', 'SUV'),
(2022, 'Mercedes-Benz', 'Mercedes-AMG GLE Coupe', 'SUV'),
(2022, 'Mercedes-Benz', 'Mercedes-EQ EQB', 'SUV'),
(2022, 'Mercedes-Benz', 'Mercedes-EQ EQS', 'Sedan'),
(2022, 'Mercedes-Benz', 'S-Class', 'Sedan'),
(2022, 'MINI', 'Clubman', 'Hatchback'),
(2022, 'MINI', 'Convertible', 'Convertible'),
(2022, 'MINI', 'Countryman', 'SUV'),
(2022, 'MINI', 'Hardtop 2 Door', 'Hatchback'),
(2022, 'MINI', 'Hardtop 4 Door', 'Hatchback'),
(2022, 'Mitsubishi', 'Eclipse Cross', 'SUV'),
(2022, 'Mitsubishi', 'Mirage', 'Hatchback'),
(2022, 'Mitsubishi', 'Outlander', 'SUV'),
(2022, 'Mitsubishi', 'Outlander PHEV', 'SUV'),
(2022, 'Mitsubishi', 'Outlander Sport', 'SUV'),
(2022, 'Nissan', '400Z', 'Coupe'),
(2022, 'Nissan', 'Altima', 'Sedan'),
(2022, 'Nissan', 'Ariya', 'SUV'),
(2022, 'Nissan', 'Armada', 'SUV'),
(2022, 'Nissan', 'Frontier Crew Cab', 'Pickup'),
(2022, 'Nissan', 'Frontier King Cab', 'Pickup'),
(2022, 'Nissan', 'GT-R', 'Coupe'),
(2022, 'Nissan', 'Kicks', 'SUV'),
(2022, 'Nissan', 'LEAF', 'Hatchback'),
(2022, 'Nissan', 'Maxima', 'Sedan'),
(2022, 'Nissan', 'Murano', 'SUV'),
(2022, 'Nissan', 'Pathfinder', 'SUV'),
(2022, 'Nissan', 'Rogue', 'SUV'),
(2022, 'Nissan', 'Rogue Sport', 'SUV'),
(2022, 'Nissan', 'Sentra', 'Sedan'),
(2022, 'Nissan', 'Titan King Cab', 'Pickup'),
(2022, 'Nissan', 'Versa', 'Sedan'),
(2022, 'Polestar', '2', 'Hatchback'),
(2022, 'Porsche', '718 Boxster', 'Convertible'),
(2022, 'Porsche', '718 Cayman', 'Coupe'),
(2022, 'Porsche', '718 Spyder', 'Convertible'),
(2022, 'Porsche', '911', 'Coupe'),
(2022, 'Porsche', 'Cayenne', 'SUV'),
(2022, 'Porsche', 'Cayenne Coupe', 'SUV'),
(2022, 'Porsche', 'Macan', 'SUV'),
(2022, 'Porsche', 'Panamera', 'Sedan'),
(2022, 'Porsche', 'Taycan', 'Sedan'),
(2022, 'Porsche', 'Taycan Cross Turismo', 'Coupe'),
(2022, 'Ram', '1500 Classic Quad Cab', 'Pickup'),
(2022, 'Ram', '1500 Quad Cab', 'Pickup'),
(2022, 'Ram', '2500 Crew Cab', 'Pickup'),
(2022, 'Ram', '2500 Mega Cab', 'Pickup'),
(2022, 'Ram', '2500 Regular Cab', 'Pickup'),
(2022, 'Ram', '3500 Crew Cab', 'Pickup'),
(2022, 'Ram', 'ProMaster Cargo Van', 'Van/Minivan'),
(2022, 'Rivian', 'R1S', 'SUV'),
(2022, 'Rivian', 'R1T', 'Pickup'),
(2022, 'Subaru', 'Ascent', 'SUV'),
(2022, 'Subaru', 'BRZ', 'Coupe'),
(2022, 'Subaru', 'Crosstrek', 'SUV'),
(2022, 'Subaru', 'Forester', 'SUV'),
(2022, 'Subaru', 'Impreza', 'Sedan & Wagon'),
(2022, 'Subaru', 'Legacy', 'Sedan'),
(2022, 'Subaru', 'Outback', 'SUV'),
(2022, 'Subaru', 'WRX', 'Sedan'),
(2022, 'Tesla', 'Cybertruck', 'Pickup'),
(2022, 'Tesla', 'Model 3', 'Sedan'),
(2022, 'Tesla', 'Model S', 'Sedan'),
(2022, 'Tesla', 'Model X', 'SUV'),
(2022, 'Tesla', 'Model Y', 'SUV'),
(2022, 'Toyota', '4Runner', 'SUV'),
(2022, 'Toyota', '86', 'Coupe'),
(2022, 'Toyota', 'Avalon', 'Sedan'),
(2022, 'Toyota', 'Avalon Hybrid', 'Sedan'),
(2022, 'Toyota', 'Camry', 'Sedan'),
(2022, 'Toyota', 'Camry Hybrid', 'Sedan'),
(2022, 'Toyota', 'C-HR', 'SUV'),
(2022, 'Toyota', 'Corolla', 'Sedan'),
(2022, 'Toyota', 'Corolla Cross', 'SUV'),
(2022, 'Toyota', 'Corolla Hatchback', 'Hatchback'),
(2022, 'Toyota', 'Corolla Hybrid', 'Sedan'),
(2022, 'Toyota', 'GR Supra', 'Coupe'),
(2022, 'Toyota', 'Highlander', 'SUV'),
(2022, 'Toyota', 'Highlander Hybrid', 'SUV'),
(2022, 'Toyota', 'Mirai', 'Sedan'),
(2022, 'Toyota', 'Prius', 'Hatchback'),
(2022, 'Toyota', 'Prius Prime', 'Hatchback'),
(2022, 'Toyota', 'RAV4', 'SUV'),
(2022, 'Toyota', 'RAV4 Hybrid', 'SUV'),
(2022, 'Toyota', 'RAV4 Prime', 'SUV'),
(2022, 'Toyota', 'Sequoia', 'SUV'),
(2022, 'Toyota', 'Sienna', 'Van/Minivan'),
(2022, 'Toyota', 'Tacoma Access Cab', 'Pickup'),
(2022, 'Toyota', 'Tacoma Double Cab', 'Pickup'),
(2022, 'Toyota', 'Tundra CrewMax', 'Pickup'),
(2022, 'Toyota', 'Venza', 'SUV'),
(2022, 'Volkswagen', 'Arteon', 'Sedan'),
(2022, 'Volkswagen', 'Atlas', 'SUV'),
(2022, 'Volkswagen', 'Atlas Cross Sport', 'SUV'),
(2022, 'Volkswagen', 'Golf GTI', 'Hatchback'),
(2022, 'Volkswagen', 'ID.4', 'SUV'),
(2022, 'Volkswagen', 'Jetta', 'Sedan'),
(2022, 'Volkswagen', 'Passat', 'Sedan'),
(2022, 'Volkswagen', 'Taos', 'SUV'),
(2022, 'Volkswagen', 'Tiguan', 'SUV'),
(2022, 'Volvo', 'C40 Recharge', 'SUV'),
(2022, 'Volvo', 'S60', 'Sedan'),
(2022, 'Volvo', 'S90', 'Sedan'),
(2022, 'Volvo', 'V60', 'Wagon'),
(2022, 'Volvo', 'V90', 'Wagon'),
(2022, 'Volvo', 'XC40', 'SUV'),
(2022, 'Volvo', 'XC40 Recharge', 'SUV'),
(2022, 'Volvo', 'XC60', 'SUV'),
(2022, 'Volvo', 'XC90', 'SUV'),
(2021, 'Acura', 'ILX', 'Sedan'),
(2021, 'Acura', 'NSX', 'Coupe'),
(2021, 'Acura', 'RDX', 'SUV'),
(2021, 'Acura', 'TLX', 'Sedan'),
(2021, 'Alfa Romeo', 'Giulia', 'Sedan'),
(2021, 'Alfa Romeo', 'Stelvio', 'SUV'),
(2021, 'Aston Martin', 'DB11', 'Coupe & Convertible'),
(2021, 'Aston Martin', 'DBS Superleggera', 'Coupe & Convertible'),
(2021, 'Aston Martin', 'DBX', 'SUV'),
(2021, 'Aston Martin', 'Vantage', 'Coupe'),
(2021, 'Audi', 'A4', 'Sedan'),
(2021, 'Audi', 'A4 allroad', 'Wagon'),
(2021, 'Audi', 'A5', 'Coupe & Sedan & Convertible'),
(2021, 'Audi', 'A6', 'Sedan'),
(2021, 'Audi', 'A6 allroad', 'Wagon'),
(2021, 'Audi', 'A7', 'Sedan'),
(2021, 'Audi', 'A8', 'Sedan'),
(2021, 'Audi', 'e-tron', 'SUV'),
(2021, 'Audi', 'e-tron Sportback', 'SUV'),
(2021, 'Audi', 'Q3', 'SUV'),
(2021, 'Audi', 'Q5', 'SUV'),
(2021, 'Audi', 'Q5 Sportback', 'SUV'),
(2021, 'Audi', 'Q7', 'SUV'),
(2021, 'Audi', 'Q8', 'SUV'),
(2021, 'Audi', 'R8', 'Coupe & Convertible'),
(2021, 'Audi', 'RS 5', 'Sedan & Coupe'),
(2021, 'Audi', 'RS 6', 'Wagon'),
(2021, 'Audi', 'RS 7', 'Sedan'),
(2021, 'Audi', 'RS Q8', 'SUV'),
(2021, 'Audi', 'S4', 'Sedan'),
(2021, 'Audi', 'S5', 'Convertible & Coupe & Sedan'),
(2021, 'Audi', 'S6', 'Sedan'),
(2021, 'Audi', 'S7', 'Sedan'),
(2021, 'Audi', 'S8', 'Sedan'),
(2021, 'Audi', 'SQ5', 'SUV'),
(2021, 'Audi', 'SQ5 Sportback', 'SUV'),
(2021, 'Audi', 'SQ7', 'SUV'),
(2021, 'Audi', 'SQ8', 'SUV'),
(2021, 'Audi', 'TT', 'Coupe'),
(2021, 'Bentley', 'Bentayga', 'SUV'),
(2021, 'Bentley', 'Continental GT', 'Convertible'),
(2021, 'Bentley', 'Flying Spur', 'Sedan'),
(2021, 'BMW', '2 Series', 'Sedan & Coupe & Convertible'),
(2021, 'BMW', '3 Series', 'Sedan'),
(2021, 'BMW', '4 Series', 'Coupe & Convertible'),
(2021, 'BMW', '5 Series', 'Sedan'),
(2021, 'BMW', '7 Series', 'Sedan'),
(2021, 'BMW', '8 Series', 'Sedan & Convertible & Coupe'),
(2021, 'BMW', 'i3', 'Hatchback'),
(2021, 'BMW', 'M2', 'Coupe'),
(2021, 'BMW', 'M3', 'Sedan'),
(2021, 'BMW', 'M4', 'Coupe'),
(2021, 'BMW', 'M5', 'Sedan'),
(2021, 'BMW', 'M8', 'Hatchback'),
(2021, 'BMW', 'X1', 'SUV'),
(2021, 'BMW', 'X2', 'SUV'),
(2021, 'BMW', 'X3', 'SUV'),
(2021, 'BMW', 'X3 M', 'SUV'),
(2021, 'BMW', 'X4', 'SUV'),
(2021, 'BMW', 'X4 M', 'SUV'),
(2021, 'BMW', 'X5', 'SUV'),
(2021, 'BMW', 'X5 M', 'SUV'),
(2021, 'BMW', 'X6', 'SUV'),
(2021, 'BMW', 'X6 M', 'SUV'),
(2021, 'BMW', 'X7', 'SUV'),
(2021, 'BMW', 'Z4', 'Convertible'),
(2021, 'Buick', 'Enclave', 'SUV'),
(2021, 'Buick', 'Encore', 'SUV'),
(2021, 'Buick', 'Encore GX', 'SUV'),
(2021, 'Buick', 'Envision', 'SUV'),
(2021, 'Cadillac', 'CT4', 'Sedan'),
(2021, 'Cadillac', 'CT5', 'Sedan'),
(2021, 'Cadillac', 'Escalade', 'SUV'),
(2021, 'Cadillac', 'Escalade ESV', 'SUV'),
(2021, 'Cadillac', 'XT4', 'SUV'),
(2021, 'Cadillac', 'XT5', 'SUV'),
(2021, 'Cadillac', 'XT6', 'SUV'),
(2021, 'Chevrolet', 'Blazer', 'SUV'),
(2021, 'Chevrolet', 'Bolt EV', 'Hatchback'),
(2021, 'Chevrolet', 'Camaro', 'Coupe & Convertible'),
(2021, 'Chevrolet', 'Colorado Crew Cab', 'Pickup'),
(2021, 'Chevrolet', 'Colorado Extended Cab', 'Pickup'),
(2021, 'Chevrolet', 'Corvette', 'Convertible & Coupe'),
(2021, 'Chevrolet', 'Equinox', 'SUV'),
(2021, 'Chevrolet', 'Express 2500 Cargo', 'Van/Minivan'),
(2021, 'Chevrolet', 'Express 2500 Passenger', 'Van/Minivan'),
(2021, 'Chevrolet', 'Express 3500 Cargo', 'Van/Minivan'),
(2021, 'Chevrolet', 'Express 3500 Passenger', 'Van/Minivan'),
(2021, 'Chevrolet', 'Malibu', 'Sedan'),
(2021, 'Chevrolet', 'Silverado 1500 Crew Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 1500 Double Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 1500 Regular Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 2500 HD Crew Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 2500 HD Double Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 2500 HD Regular Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 3500 HD Crew Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 3500 HD Double Cab', 'Pickup'),
(2021, 'Chevrolet', 'Silverado 3500 HD Regular Cab', 'Pickup'),
(2021, 'Chevrolet', 'Spark', 'Hatchback'),
(2021, 'Chevrolet', 'Suburban', 'SUV'),
(2021, 'Chevrolet', 'Tahoe', 'SUV'),
(2021, 'Chevrolet', 'Trailblazer', 'SUV'),
(2021, 'Chevrolet', 'Traverse', 'SUV'),
(2021, 'Chevrolet', 'Trax', 'SUV'),
(2021, 'Chrysler', '300', 'Sedan'),
(2021, 'Chrysler', 'Pacifica', 'Van/Minivan'),
(2021, 'Chrysler', 'Pacifica Hybrid', 'Van/Minivan'),
(2021, 'Chrysler', 'Voyager', 'Van/Minivan'),
(2021, 'Dodge', 'Challenger', 'Coupe'),
(2021, 'Dodge', 'Charger', 'Sedan'),
(2021, 'Dodge', 'Durango', 'SUV'),
(2021, 'Ferrari', '488 Pista', 'Coupe & Convertible'),
(2021, 'Ferrari', '812 GTS', 'Convertible'),
(2021, 'Ferrari', '812 Superfast', 'Coupe'),
(2021, 'Ferrari', 'F8', 'Coupe & Convertible'),
(2021, 'Ferrari', 'Portofino', 'Convertible'),
(2021, 'Ferrari', 'Roma', 'Coupe'),
(2021, 'Ferrari', 'SF90', 'Coupe & Convertible'),
(2021, 'FIAT', '500X', 'SUV'),
(2021, 'Ford', 'Bronco', 'SUV'),
(2021, 'Ford', 'Bronco Sport', 'SUV'),
(2021, 'Ford', 'EcoSport', 'SUV'),
(2021, 'Ford', 'Edge', 'SUV'),
(2021, 'Ford', 'Escape', 'SUV'),
(2021, 'Ford', 'Expedition', 'SUV'),
(2021, 'Ford', 'Expedition MAX', 'SUV'),
(2021, 'Ford', 'Explorer', 'SUV'),
(2021, 'Ford', 'F150 Regular Cab', 'Pickup'),
(2021, 'Ford', 'F150 Super Cab', 'Pickup'),
(2021, 'Ford', 'F150 SuperCrew Cab', 'Pickup'),
(2021, 'Ford', 'F250 Super Duty Crew Cab', 'Pickup'),
(2021, 'Ford', 'F250 Super Duty Regular Cab', 'Pickup'),
(2021, 'Ford', 'F250 Super Duty Super Cab', 'Pickup'),
(2021, 'Ford', 'F350 Super Duty Crew Cab', 'Pickup'),
(2021, 'Ford', 'F350 Super Duty Regular Cab', 'Pickup'),
(2021, 'Ford', 'F350 Super Duty Super Cab', 'Pickup'),
(2021, 'Ford', 'F450 Super Duty Crew Cab', 'Pickup'),
(2021, 'Ford', 'Mustang', 'Coupe & Convertible'),
(2021, 'Ford', 'Mustang MACH-E', 'SUV'),
(2021, 'Ford', 'Ranger SuperCab', 'Pickup'),
(2021, 'Ford', 'Ranger SuperCrew', 'Pickup'),
(2021, 'Ford', 'Transit 150 Cargo Van', 'Van/Minivan'),
(2021, 'Ford', 'Transit 150 Crew Van', 'Van/Minivan'),
(2021, 'Ford', 'Transit 250 Cargo Van', 'Van/Minivan'),
(2021, 'Ford', 'Transit 350 Crew Van', 'Van/Minivan'),
(2021, 'Ford', 'Transit 350 HD Cargo Van', 'Van/Minivan'),
(2021, 'Ford', 'Transit Connect Cargo Van', 'Van/Minivan'),
(2021, 'Ford', 'Transit Connect Passenger Wagon', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 1500 Cargo', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 1500 Passenger', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 2500 Cargo', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 2500 Crew', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 2500 Passenger', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 3500 Cargo', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 3500 Crew', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 3500 XD Crew', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 3500XD Cargo', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 4500 Cargo', 'Van/Minivan'),
(2021, 'Freightliner', 'Sprinter 4500 Crew', 'Van/Minivan'),
(2021, 'Genesis', 'G70', 'Sedan'),
(2021, 'Genesis', 'G80', 'Sedan'),
(2021, 'Genesis', 'G90', 'Sedan'),
(2021, 'Genesis', 'GV80', 'SUV'),
(2021, 'GMC', 'Acadia', 'SUV'),
(2021, 'GMC', 'Canyon Crew Cab', 'Pickup'),
(2021, 'GMC', 'Canyon Extended Cab', 'Pickup'),
(2021, 'GMC', 'Savana 2500 Cargo', 'Van/Minivan'),
(2021, 'GMC', 'Savana 2500 Passenger', 'Van/Minivan'),
(2021, 'GMC', 'Savana 3500 Cargo', 'Van/Minivan'),
(2021, 'GMC', 'Savana 3500 Passenger', 'Van/Minivan'),
(2021, 'GMC', 'Sierra 1500 Crew Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 1500 Double Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 1500 Regular Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 2500 HD Crew Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 2500 HD Double Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 2500 HD Regular Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 3500 HD Crew Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 3500 HD Double Cab', 'Pickup'),
(2021, 'GMC', 'Sierra 3500 HD Regular Cab', 'Pickup'),
(2021, 'GMC', 'Terrain', 'SUV'),
(2021, 'GMC', 'Yukon', 'SUV'),
(2021, 'GMC', 'Yukon XL', 'SUV'),
(2021, 'Honda', 'Accord', 'Sedan'),
(2021, 'Honda', 'Accord Hybrid', 'Sedan'),
(2021, 'Honda', 'Civic', 'Sedan & Hatchback'),
(2021, 'Honda', 'Civic Type R', 'Hatchback'),
(2021, 'Honda', 'Clarity Fuel Cell', 'Sedan'),
(2021, 'Honda', 'Clarity Plug-in Hybrid', 'Sedan'),
(2021, 'Honda', 'CR-V', 'SUV'),
(2021, 'Honda', 'CR-V Hybrid', 'SUV'),
(2021, 'Honda', 'HR-V', 'SUV'),
(2021, 'Honda', 'Insight', 'Sedan'),
(2021, 'Honda', 'Odyssey', 'Van/Minivan'),
(2021, 'Honda', 'Passport', 'SUV'),
(2021, 'Honda', 'Pilot', 'SUV'),
(2021, 'Honda', 'Ridgeline', 'Pickup'),
(2021, 'Hyundai', 'Accent', 'Sedan'),
(2021, 'Hyundai', 'Elantra', 'Sedan'),
(2021, 'Hyundai', 'Ioniq Electric', 'Hatchback'),
(2021, 'Hyundai', 'Ioniq Hybrid', 'Hatchback'),
(2021, 'Hyundai', 'Ioniq Plug-in Hybrid', 'Hatchback'),
(2021, 'Hyundai', 'Kona', 'SUV'),
(2021, 'Hyundai', 'Kona Electric', 'SUV'),
(2021, 'Hyundai', 'NEXO', 'SUV'),
(2021, 'Hyundai', 'Palisade', 'SUV'),
(2021, 'Hyundai', 'Santa Fe', 'SUV'),
(2021, 'Hyundai', 'Santa Fe Hybrid', 'SUV'),
(2021, 'Hyundai', 'Sonata', 'Sedan'),
(2021, 'Hyundai', 'Sonata Hybrid', 'Sedan'),
(2021, 'Hyundai', 'Tucson', 'SUV'),
(2021, 'Hyundai', 'Veloster', 'Coupe'),
(2021, 'Hyundai', 'Venue', 'SUV'),
(2021, 'INFINITI', 'Q50', 'Sedan'),
(2021, 'INFINITI', 'Q60', 'Coupe'),
(2021, 'INFINITI', 'QX50', 'SUV'),
(2021, 'INFINITI', 'QX80', 'SUV'),
(2021, 'Jaguar', 'E-PACE', 'SUV'),
(2021, 'Jaguar', 'F-PACE', 'SUV'),
(2021, 'Jaguar', 'F-TYPE', 'Coupe & Convertible'),
(2021, 'Jaguar', 'I-PACE', 'SUV'),
(2021, 'Jaguar', 'XF', 'Sedan'),
(2021, 'Jeep', 'Cherokee', 'SUV'),
(2021, 'Jeep', 'Compass', 'SUV'),
(2021, 'Jeep', 'Gladiator', 'Pickup'),
(2021, 'Jeep', 'Grand Cherokee', 'SUV'),
(2021, 'Jeep', 'Grand Cherokee L', 'SUV'),
(2021, 'Jeep', 'Renegade', 'SUV'),
(2021, 'Jeep', 'Wrangler', 'SUV'),
(2021, 'Jeep', 'Wrangler Unlimited', 'SUV'),
(2021, 'Jeep', 'Wrangler Unlimited 4xe', 'SUV'),
(2021, 'Kia', 'Forte', 'Sedan'),
(2021, 'Kia', 'K5', 'Sedan'),
(2021, 'Kia', 'Niro', 'Wagon'),
(2021, 'Kia', 'Niro EV', 'Wagon'),
(2021, 'Kia', 'Niro Plug-in Hybrid', 'Wagon'),
(2021, 'Kia', 'Rio', 'Sedan & Hatchback'),
(2021, 'Kia', 'Sedona', 'Van/Minivan'),
(2021, 'Kia', 'Seltos', 'SUV'),
(2021, 'Kia', 'Sorento', 'SUV'),
(2021, 'Kia', 'Sorento Hybrid', 'SUV'),
(2021, 'Kia', 'Soul', 'Wagon'),
(2021, 'Kia', 'Sportage', 'SUV'),
(2021, 'Kia', 'Stinger', 'Sedan'),
(2021, 'Kia', 'Telluride', 'SUV'),
(2021, 'Lamborghini', 'Aventador', 'Coupe & Convertible'),
(2021, 'Lamborghini', 'Huracan', 'Coupe & Convertible'),
(2021, 'Lamborghini', 'Urus', 'SUV'),
(2021, 'Land Rover', 'Defender 110', 'SUV'),
(2021, 'Land Rover', 'Defender 90', 'SUV'),
(2021, 'Land Rover', 'Discovery', 'SUV'),
(2021, 'Land Rover', 'Discovery Sport', 'SUV'),
(2021, 'Land Rover', 'Range Rover', 'SUV'),
(2021, 'Land Rover', 'Range Rover Evoque', 'SUV'),
(2021, 'Land Rover', 'Range Rover Sport', 'SUV'),
(2021, 'Land Rover', 'Range Rover Velar', 'SUV'),
(2021, 'Lexus', 'ES', 'Sedan'),
(2021, 'Lexus', 'GX', 'SUV'),
(2021, 'Lexus', 'IS', 'Sedan'),
(2021, 'Lexus', 'LC', 'Convertible & Coupe'),
(2021, 'Lexus', 'LS', 'Sedan'),
(2021, 'Lexus', 'LX', 'SUV'),
(2021, 'Lexus', 'NX', 'SUV'),
(2021, 'Lexus', 'RC', 'Coupe'),
(2021, 'Lexus', 'RX', 'SUV'),
(2021, 'Lexus', 'UX', 'SUV'),
(2021, 'Lincoln', 'Aviator', 'SUV'),
(2021, 'Lincoln', 'Corsair', 'SUV'),
(2021, 'Lincoln', 'Nautilus', 'SUV'),
(2021, 'Lincoln', 'Navigator', 'SUV'),
(2021, 'Lincoln', 'Navigator L', 'SUV'),
(2021, 'Lotus', 'Evora GT', 'Coupe'),
(2021, 'Maserati', 'Ghibli', 'Sedan'),
(2021, 'Maserati', 'Levante', 'SUV'),
(2021, 'Maserati', 'Quattroporte', 'Sedan'),
(2021, 'MAZDA', 'CX-3', 'SUV'),
(2021, 'MAZDA', 'CX-30', 'SUV'),
(2021, 'MAZDA', 'CX-5', 'SUV'),
(2021, 'MAZDA', 'CX-9', 'SUV'),
(2021, 'MAZDA', 'MAZDA3', 'Hatchback & Sedan'),
(2021, 'MAZDA', 'MAZDA6', 'Sedan'),
(2021, 'MAZDA', 'MX-5 Miata', 'Convertible'),
(2021, 'MAZDA', 'MX-5 Miata RF', 'Convertible'),
(2021, 'Mercedes-Benz', 'A-Class', 'Sedan'),
(2021, 'Mercedes-Benz', 'C-Class', 'Coupe & Sedan & Convertible'),
(2021, 'Mercedes-Benz', 'CLA', 'Sedan'),
(2021, 'Mercedes-Benz', 'CLS', 'Sedan'),
(2021, 'Mercedes-Benz', 'E-Class', 'Sedan & Coupe & Wagon & Convertible'),
(2021, 'Mercedes-Benz', 'G-Class', 'SUV'),
(2021, 'Mercedes-Benz', 'GLA', 'SUV'),
(2021, 'Mercedes-Benz', 'GLB', 'SUV'),
(2021, 'Mercedes-Benz', 'GLC', 'SUV'),
(2021, 'Mercedes-Benz', 'GLC Coupe', 'SUV'),
(2021, 'Mercedes-Benz', 'GLE', 'SUV'),
(2021, 'Mercedes-Benz', 'GLS', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG A-Class', 'Sedan'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG C-Class', 'Coupe & Convertible & Sedan'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG CLA', 'Sedan'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG CLS', 'Sedan'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG E-Class', 'Convertible & Sedan & Coupe & Wagon'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG G-Class', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLA', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLB', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLC', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLC Coupe', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLE', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLE Coupe', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GLS', 'SUV'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG GT', 'Sedan & Convertible & Coupe'),
(2021, 'Mercedes-Benz', 'Mercedes-AMG S-Class', 'Coupe & Convertible'),
(2021, 'Mercedes-Benz', 'Mercedes-Maybach GLS', 'SUV'),
(2021, 'Mercedes-Benz', 'Metris Cargo', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Metris Passenger', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'S-Class', 'Sedan & Coupe & Convertible'),
(2021, 'Mercedes-Benz', 'Sprinter 1500 Cargo', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 1500 Passenger', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 2500 Cargo', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 2500 Crew', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 2500 Passenger', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 3500 Cargo', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 3500 Crew', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 3500 XD Cargo', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 3500 XD Crew', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 4500 Cargo', 'Van/Minivan'),
(2021, 'Mercedes-Benz', 'Sprinter 4500 Crew', 'Van/Minivan'),
(2021, 'MINI', 'Clubman', 'Hatchback'),
(2021, 'MINI', 'Convertible', 'Convertible'),
(2021, 'MINI', 'Countryman', 'SUV'),
(2021, 'MINI', 'Hardtop 2 Door', 'Hatchback'),
(2021, 'MINI', 'Hardtop 4 Door', 'Hatchback'),
(2021, 'Mitsubishi', 'Mirage', 'Hatchback'),
(2021, 'Mitsubishi', 'Mirage G4', 'Sedan'),
(2021, 'Mitsubishi', 'Outlander PHEV', 'SUV'),
(2021, 'Mitsubishi', 'Outlander Sport', 'SUV'),
(2021, 'Nissan', 'Altima', 'Sedan'),
(2021, 'Nissan', 'Armada', 'SUV'),
(2021, 'Nissan', 'Frontier Crew Cab', 'Pickup'),
(2021, 'Nissan', 'Frontier King Cab', 'Pickup'),
(2021, 'Nissan', 'GT-R', 'Coupe'),
(2021, 'Nissan', 'Kicks', 'SUV'),
(2021, 'Nissan', 'LEAF', 'Hatchback'),
(2021, 'Nissan', 'Maxima', 'Sedan'),
(2021, 'Nissan', 'Murano', 'SUV'),
(2021, 'Nissan', 'NV1500 Cargo', 'Van/Minivan'),
(2021, 'Nissan', 'NV200', 'Van/Minivan'),
(2021, 'Nissan', 'NV2500 HD Cargo', 'Van/Minivan'),
(2021, 'Nissan', 'NV3500 HD Cargo', 'Van/Minivan'),
(2021, 'Nissan', 'NV3500 HD Passenger', 'Van/Minivan'),
(2021, 'Nissan', 'Rogue', 'SUV'),
(2021, 'Nissan', 'Rogue Sport', 'SUV'),
(2021, 'Nissan', 'Sentra', 'Sedan'),
(2021, 'Nissan', 'Titan Crew Cab', 'Pickup'),
(2021, 'Nissan', 'Titan King Cab', 'Pickup'),
(2021, 'Nissan', 'TITAN XD Crew Cab', 'Pickup'),
(2021, 'Nissan', 'Versa', 'Sedan'),
(2021, 'Polestar', '1', 'Coupe'),
(2021, 'Polestar', '2', 'Hatchback'),
(2021, 'Porsche', '718 Boxster', 'Convertible'),
(2021, 'Porsche', '718 Cayman', 'Coupe'),
(2021, 'Porsche', '718 Spyder', 'Convertible'),
(2021, 'Porsche', '911', 'Coupe & Convertible'),
(2021, 'Porsche', 'Cayenne', 'SUV'),
(2021, 'Porsche', 'Cayenne Coupe', 'SUV'),
(2021, 'Porsche', 'Macan', 'SUV'),
(2021, 'Porsche', 'Panamera', 'Sedan'),
(2021, 'Porsche', 'Taycan', 'Sedan'),
(2021, 'Ram', '1500 Classic Crew Cab', 'Pickup'),
(2021, 'Ram', '1500 Classic Quad Cab', 'Pickup'),
(2021, 'Ram', '1500 Classic Regular Cab', 'Pickup'),
(2021, 'Ram', '1500 Crew Cab', 'Pickup'),
(2021, 'Ram', '1500 Quad Cab', 'Pickup'),
(2021, 'Ram', '2500 Crew Cab', 'Pickup'),
(2021, 'Ram', '2500 Mega Cab', 'Pickup'),
(2021, 'Ram', '2500 Regular Cab', 'Pickup'),
(2021, 'Ram', '3500 Crew Cab', 'Pickup'),
(2021, 'Ram', '3500 Mega Cab', 'Pickup'),
(2021, 'Ram', '3500 Regular Cab', 'Pickup'),
(2021, 'Ram', 'ProMaster Cargo Van', 'Van/Minivan'),
(2021, 'Ram', 'ProMaster City', 'Van/Minivan'),
(2021, 'Ram', 'ProMaster Window Van', 'Van/Minivan'),
(2021, 'Rivian', 'R1S', 'SUV'),
(2021, 'Rivian', 'R1T', 'Pickup'),
(2021, 'Rolls-Royce', 'Cullinan', 'SUV'),
(2021, 'Rolls-Royce', 'Dawn', 'Convertible'),
(2021, 'Rolls-Royce', 'Ghost', 'Sedan'),
(2021, 'Rolls-Royce', 'Phantom', 'Sedan'),
(2021, 'Rolls-Royce', 'Wraith', 'Coupe'),
(2021, 'Subaru', 'Ascent', 'SUV'),
(2021, 'Subaru', 'Crosstrek', 'SUV'),
(2021, 'Subaru', 'Forester', 'SUV'),
(2021, 'Subaru', 'Impreza', 'Wagon & Sedan'),
(2021, 'Subaru', 'Legacy', 'Sedan'),
(2021, 'Subaru', 'Outback', 'SUV'),
(2021, 'Subaru', 'WRX', 'Sedan'),
(2021, 'Tesla', 'Model 3', 'Sedan'),
(2021, 'Tesla', 'Model S', 'Sedan'),
(2021, 'Tesla', 'Model X', 'SUV'),
(2021, 'Tesla', 'Model Y', 'SUV'),
(2021, 'Toyota', '4Runner', 'SUV'),
(2021, 'Toyota', 'Avalon', 'Sedan'),
(2021, 'Toyota', 'Avalon Hybrid', 'Sedan'),
(2021, 'Toyota', 'Camry', 'Sedan'),
(2021, 'Toyota', 'Camry Hybrid', 'Sedan'),
(2021, 'Toyota', 'C-HR', 'SUV'),
(2021, 'Toyota', 'Corolla', 'Sedan'),
(2021, 'Toyota', 'Corolla Hatchback', 'Hatchback'),
(2021, 'Toyota', 'Corolla Hybrid', 'Sedan'),
(2021, 'Toyota', 'GR Supra', 'Coupe'),
(2021, 'Toyota', 'Highlander', 'SUV'),
(2021, 'Toyota', 'Highlander Hybrid', 'SUV'),
(2021, 'Toyota', 'Land Cruiser', 'SUV'),
(2021, 'Toyota', 'Mirai', 'Sedan'),
(2021, 'Toyota', 'Prius', 'Hatchback'),
(2021, 'Toyota', 'Prius Prime', 'Hatchback'),
(2021, 'Toyota', 'RAV4', 'SUV'),
(2021, 'Toyota', 'RAV4 Hybrid', 'SUV'),
(2021, 'Toyota', 'RAV4 Prime', 'SUV'),
(2021, 'Toyota', 'Sequoia', 'SUV'),
(2021, 'Toyota', 'Sienna', 'Van/Minivan'),
(2021, 'Toyota', 'Tacoma Access Cab', 'Pickup'),
(2021, 'Toyota', 'Tacoma Double Cab', 'Pickup'),
(2021, 'Toyota', 'Tundra CrewMax', 'Pickup'),
(2021, 'Toyota', 'Tundra Double Cab', 'Pickup'),
(2021, 'Toyota', 'Venza', 'SUV'),
(2021, 'Volkswagen', 'Arteon', 'Sedan'),
(2021, 'Volkswagen', 'Atlas', 'SUV'),
(2021, 'Volkswagen', 'Atlas Cross Sport', 'SUV'),
(2021, 'Volkswagen', 'Golf', 'Hatchback'),
(2021, 'Volkswagen', 'Golf GTI', 'Hatchback'),
(2021, 'Volkswagen', 'ID.4', 'SUV'),
(2021, 'Volkswagen', 'Jetta', 'Sedan'),
(2021, 'Volkswagen', 'Jetta GLI', 'Sedan'),
(2021, 'Volkswagen', 'Passat', 'Sedan'),
(2021, 'Volkswagen', 'Tiguan', 'SUV'),
(2021, 'Volvo', 'S60', 'Sedan'),
(2021, 'Volvo', 'S90', 'Sedan'),
(2021, 'Volvo', 'V60', 'Wagon'),
(2021, 'Volvo', 'V90', 'Wagon'),
(2021, 'Volvo', 'XC40', 'SUV'),
(2021, 'Volvo', 'XC40 Recharge', 'SUV'),
(2021, 'Volvo', 'XC60', 'SUV'),
(2021, 'Volvo', 'XC90', 'SUV');
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

```



## html output

```
[{"year":2022,"make":"Acura","model":"ILX","body_styles":"Sedan"},
{"year":2022,"make":"Acura","model":"MDX","body_styles":"SUV"},
{"year":2022,"make":"Acura","model":"RDX","body_styles":"SUV"},
{"year":2022,"make":"Acura","model":"TLX","body_styles":"Sedan"},
{"year":2022,"make":"Alfa Romeo","model":"Giulia","body_styles":"Sedan"},

<!-- NOTE THIS IS AN EXAMPLE OF JUST A FEW OF THE FIRST RECORDS FROM THE OUTPUTTED WEB PAGE -->
```

