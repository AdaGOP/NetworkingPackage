# NetworkingPackage
This package will help you to create networking layer. You can expand the layer from this package

## NetworkService
This code cover all about the HTTPMethod, HTTPHeader, EndPointType protocol, NetworkError and NetworkDelegate. Try to add more properties based on what you need for your project. For example, if you need POST method, add a new case on HTTPMethod. It will be good if you move all the function to different swift file, so you can discover the method easily.

## PhotoEndPoint
This is an **example** of how to use EndPoint type on the Network Service.

## NetworkManager
This is the network manager that will handle the request, update the request based on what you want to do. The result of the request will be Data, you need to transform the data to network model

## PhotoNetworkModel
This is an **example** of network model that will help you to decode the result of the network.

## CollectionViewController
This is an **example** on how do we use it on view controller level. You can see how do we decode the data to network model
