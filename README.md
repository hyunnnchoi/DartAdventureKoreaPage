# DartAdventureKoreaPage

Welcome to the **DartAdventureKoreaPage** project! 🎯✨

Visit https://hyunnnchoi.github.io/DartAdventureKoreaPage/

This project generates random coordinates within South Korea's land area and displays them on Google Maps. It's perfect for spontaneous travel enthusiasts looking for their next adventure spot in South Korea!

## Features

- Generates random coordinates within South Korea's land area.
- Displays the coordinates on an interactive Google Map.
- Provides a link to open the location in Google Maps.

## Installation

To get started, simply clone the repository and open the `index.html` file in your web browser.

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/DartAdventureKoreaPage.git
    cd DartAdventureKoreaPage
    ```

2. Open the `index.html` file in your favorite web browser:

    ```bash
    open index.html
    ```

    Or double-click the `index.html` file to open it.

## Usage

The web page will display a random travel destination within South Korea on Google Maps. You can generate a new random destination by clicking the "Generate New Coordinate" button.

## Code Explanation

The main logic for generating random coordinates and displaying them on Google Maps is implemented in the `index.html` file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Travel Destination</title>
    <style>
        #map {
            height: 500px;
            width: 100%;
            border: 0;
        }
    </style>
    <script>
        function generateRandomCoordinate() {
            // 한국 육지 범위 (대략적인 값)
            const minLatitude = 34.0;
            const maxLatitude = 38.5;
            const minLongitude = 126.0;
            const maxLongitude = 129.5;

            let randomLatitude, randomLongitude;
            while (true) {
                randomLatitude = (Math.random() * (maxLatitude - minLatitude) + minLatitude).toFixed(6);
                randomLongitude = (Math.random() * (maxLongitude - minLongitude) + minLongitude).toFixed(6);

                // 육지 범위에 속하는지 확인 (필요시 육지 경계 정보로 정확하게 조정 가능)
                if ((randomLatitude >= 34.0 && randomLatitude <= 38.5) && (randomLongitude >= 126.0 && randomLongitude <= 129.5)) {
                    break;
                }
            }

            return { latitude: parseFloat(randomLatitude), longitude: parseFloat(randomLongitude) };
        }

        function displayRandomCoordinate() {
            const coordinate = generateRandomCoordinate();
            const zoomLevel = 12; // 원하는 줌 레벨 설정
            const googleMapsUrl = `https://www.google.com/maps?q=${coordinate.latitude},${coordinate.longitude}&z=${zoomLevel}&output=embed`;
            document.getElementById('coordinate').innerText = `Latitude: ${coordinate.latitude}, Longitude: ${coordinate.longitude}`;
            document.getElementById('googleMapsLink').href = googleMapsUrl;
            document.getElementById('googleMapsLink').innerText = `Open in Google Maps`;
            document.getElementById('map').src = googleMapsUrl;
        }

        window.onload = displayRandomCoordinate;
    </script>
</head>
<body>
    <h1>Random Travel Destination</h1>
    <p id="coordinate"></p>
    <a id="googleMapsLink" href="#" target="_blank"></a>
    <iframe id="map" src="https://www.google.com/maps?q=37.5665,126.9780&z=10&output=embed" frameborder="0" allowfullscreen></iframe>
    <button onclick="displayRandomCoordinate()">Generate New Coordinate</button>
</body>
</html>
