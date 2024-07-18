# Credit Card Scanner

This project is a web-based credit card scanner that uses the device's camera to capture and extract credit card information.

## Features

- Real-time camera preview
- Automatic credit card number, expiry date, and CVV detection
- Integration with React Native WebView

## Technologies Used

- HTML5
- JavaScript (ES6+)
- [Tesseract.js](https://github.com/naptha/tesseract.js) for Optical Character Recognition (OCR)

## How It Works

1. The application accesses the device's rear camera using the `getUserMedia` API.
2. It captures frames from the video stream every second.
3. Each frame is processed using Tesseract.js to perform OCR.
4. The extracted text is parsed to identify credit card information.
5. When valid card information is detected, it's sent to the React Native app via `postMessage`.

## Setup

1. Include this HTML file in your React Native WebView component.
2. Ensure that your React Native app has the necessary permissions to access the device's camera.
3. Handle the `postMessage` event in your React Native code to receive the scanned card information.

## Usage in React Native

```jsx
import React from 'react';
import { WebView } from 'react-native-webview';

const CreditCardScanner = () => {
  const handleMessage = (event) => {
    const cardData = JSON.parse(event.nativeEvent.data);
    console.log('Card data:', cardData);
    // Process the card data as needed
  };

  return (
    <WebView
      source={{ html: /* Insert the HTML code here */ }}
      onMessage={handleMessage}
      javaScriptEnabled={true}
      domStorageEnabled={true}
      mediaPlaybackRequiresUserAction={false}
      allowsInlineMediaPlayback={true}
    />
  );
};

export default CreditCardScanner;
```

## Security Considerations

- This application processes sensitive financial information. Ensure that you handle and transmit this data securely.
- Consider implementing additional security measures such as encryption when storing or transmitting card data.
- Comply with relevant data protection regulations and payment card industry standards.

## Limitations

- The accuracy of OCR depends on factors such as lighting conditions, camera quality, and card design.
- This solution may not work reliably for all types of credit cards or in all environments.

## Future Improvements

- Implement error handling and user feedback for failed scans.
- Add a user interface for better guidance during scanning.
- Optimize OCR performance and accuracy.
