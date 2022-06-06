import Foundation

class NetworkManager: NSObject {
    private lazy var session: URLSession = {
        let configuration = URLSessionConfiguration.default
        configuration.waitsForConnectivity = true
        return URLSession(configuration: configuration,
                          delegate: self, delegateQueue: nil)
    }()
    
    var endPoint: EndPointType?
    var networkDelegate: NetworkDelegate?
    
    func createRequest(with endPoint: EndPointType) {
        self.endPoint = endPoint
        
        // Construct a URL by assigning its parts to a URLComponents value
        var components = URLComponents()
        components.scheme = "https"
        components.host = endPoint.baseUrl
        components.path = endPoint.path
        
        guard let url = components.url else {
            networkDelegate?.onResponse(from: nil, result: .failure(.missingUrl))
            return
        }
        
        // Create the request to url
        var request = URLRequest(url: url)
        request.httpMethod = endPoint.method.rawValue
        
        // Set the headers to request
        if let headers = endPoint.headers {
            for (key, value) in headers {
                request.addValue(value, forHTTPHeaderField: key)
            }
        }
        
        // Assign the request to the session as a task
        let task = session.dataTask(with: request)
        
        // Run the task
        task.resume()
        
    }
}

extension NetworkManager: URLSessionDataDelegate {
    func urlSession(_ session: URLSession, dataTask: URLSessionDataTask, didReceive response: URLResponse,
                    completionHandler: @escaping (URLSession.ResponseDisposition) -> Void) {
        
        guard let response = response as? HTTPURLResponse,
              (200...299).contains(response.statusCode) else {
                  completionHandler(.cancel)
                  return
              }
        completionHandler(.allow)
    }
    
    func urlSession(_ session: URLSession, dataTask: URLSessionDataTask, didReceive data: Data) {
        guard let endPoint = self.endPoint else {
            self.networkDelegate?.onResponse(from: nil, result: .failure(NetworkError.failed))
            return
        }
        self.networkDelegate?.onResponse(from: endPoint, result: .success(data))
    }
    
    func urlSession(_ session: URLSession, task: URLSessionTask, didCompleteWithError error: Error?) {
        if let _ = error {
            self.networkDelegate?.onResponse(from: nil, result: .failure(NetworkError.failed))
        }
    }
}
