If you receive `confirmSignUp` as a next step, sign up could not proceed without confirming user information such as email or phone number. The next step is to invoke the `confirmSignUp` API and follow the confirm signup flow.

<amplify-block-switcher>

<amplify-block name="Listener (iOS 11+)">

```swift
func confirmSignUp(for username: String, with confirmationCode: String) {
    Amplify.Auth.confirmSignUp(for: username, confirmationCode: confirmationCode) { result in
        switch result {
        case .success:
            print("Confirm signUp succeeded")
        case .failure(let error):
            print("An error occurred while confirming sign up \(error)")
        }
    }
}
```

</amplify-block>

<amplify-block name="Combine (iOS 13+)">

```swift
func confirmSignUp(for username: String, with confirmationCode: String) -> AnyCancellable {
    Amplify.Auth.confirmSignUp(for: username, confirmationCode: confirmationCode)
        .resultPublisher
        .sink {
            if case let .failure(authError) = $0 {
                print("An error occurred while confirming sign up \(authError)")
            }
        }
        receiveValue: { _ in
            print("Confirm signUp succeeded")
        }
}
```

</amplify-block>

</amplify-block-switcher>