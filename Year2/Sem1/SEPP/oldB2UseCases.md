### Adopt Tree
A precondition to this use case is that the use should be logged in. A guest user cannot adopt a tree. Another pre-condition is that the cart isn’t empty. The user shouldn’t be able to adopt a tree if at least 1 tree isn’t selected. A postcondition is that after the transaction, the tree/trees adopted should be saved to that user. A normal flow of events may look like: The user selects adopt the trees that they have chosen which have been added to a cart. They will then go through with the transaction and make payment. The ‘PaymentSystem’ extends this use case. If the payment is successful, the tree is saved to the user's adopted trees.

### Company Donates
This use case is responsible for the social media aspect of the system. This use case is a part of the ‘PortalSystem’ of the overall system. The primary actor is ‘User’, who initiates this use case. A precondition to this use case is that the user is logged in. Without being logged in, the user shouldn’t be able to interact with any community posts. A postcondition is that the interaction should be saved, so it can be viewed again by the user or other users. A normal flow of events may look like: A user may type a comment on another user's post or they may like another user's post. These interactions will be saved to the system in relation to the user.

### Educational Material
A precondition to this use case is that the user is either a logged in user or a guest user. A standard flow of events may look like: The user selects the education section in the system. The system then displays the relevant information. The user can navigate different parts they want.

### Rewards System
Didn't have an old use case spec