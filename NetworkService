import Foundation

typealias HTTPHeaders = [String:String]

enum HTTPMethod: String {
    case get = "GET"
}

protocol EndPointType{
    var baseUrl: String { get }
    var path: String { get }
    var method: HTTPMethod { get }
    var headers: HTTPHeaders? { get }
}

enum NetworkError: String, Error {
    case missingUrl = "URL is missing"
    case decodingFailed = "Decoding failed"
    case authenticationError = "You need to be authenticated first or you not in Academy"
    case badRequest = "Bad request"
    case outdated = "The url you requested is outdated."
    case failed = "Network request failed."
    case noData = "Response returned with no data to decode."
    case unableToDecode = "We could not decode the response."
    case userExist = "User already exist"
    case expiredToken = "Expired Token"
}

protocol NetworkDelegate: AnyObject {
    func onResponse(from endPoint: EndPointType?, result: Result<Data, NetworkError>)
}
