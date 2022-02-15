---
theme: default
background: >-
  https://images.unsplash.com/photo-1587620962725-abab7fe55159?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1631&q=80
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
title: Unit Testing 101
---

# Software Testing 101

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer bg-white bg-opacity-25">
    By Srinivas, Software Craftsperson @ EverestEngineering
  </span>
</div>

<style>
  h1 {
    color: white;
  }
</style>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# Agenda

We are going to cover

- **Why do we have to write automated tests ?**
- **Types of tests ( Test Pyramid )**
- **Are we really writing unit tests ?**
- **Writing testable code**
- **Types of test doubles**
- **Mocking best practices**
- **Integration testing**
- **e2e testing**


---

# Why do we have to write automated tests ?

<v-clicks>

- To see if the system satisfies the software requirements
  
- To catch regressions, if any
  
- To reduce/eliminate manual testing efforts
  
- To refactor without fear of breaking things
  
- To get good night sleep
  
- To help newcomers understand the codebase

</v-clicks>


---
layout: two-cols
---
# Types of tests

- Unit tests
- Integration tests
- e2e tests

::right::
<figure>
  <img src="images/testpyramid.jpg">
  <figcaption>Test Pyramid</figcaption>
</figure>

---
layout: two-cols
---
# The four pillers of a good test portfolio

<v-clicks>
  
  - Protection against regressions
  
  - Resistance to refactoring
  
  - Fast feedback
  
  - Maintainability

</v-clicks>

::right::
<v-click>
<figure>
  <img src="images/balancedtests.jpg">
</figure>
</v-click>

---

# What is unit test ?

<v-click>

#### A unit test is a piece of code

</v-click>
<v-clicks>

  - that verifies a small piece of code called the unit

  - and does that quickly

  - and does it in an isolated manner

</v-clicks>

<style>
  h4 {
    color: goldenrod;
    padding: 10px 0;
  }
  ul {
    padding: 0 10px;
  }
</style>

---

# Writing Testable code

<v-click>

```csharp {all|1-15|16-18|all}
class EmailService {
  public void sendEmail(string from, string to, string subject, string body){
    // sends email over network...
  }
}

class RegistrationService {

  public void register(string username, string email, string password){
    // logic to create user in database
    var emailService = new EmailService();
    emailService.sendEmail("team@website.com", email, "Welcome onboard", "We are happy to have you onboard")
  }
}

// in entry point
var registrationService = new RegistrationService();
registrationService.register("developer", "dummyemail@gmail.com", "hashedpassword");
```

</v-click>

---

# Writing Testable code (continued...)


<v-click>

> All problems in computer science can be solved by adding another level of indirection.
>
> -- <cite>David Wheeler</cite>

</v-click>

<v-click>

#### Dependency Inversion

</v-click>

---

# Writing Testable code (continued...)


> All problems in computer science can be solved by adding another level of indirection.
>
> -- <cite>David Wheeler</cite>

<v-click>

```csharp {all|1-3|5-9|all}
interface IEmailService {
  void sendEmail(string from, string to, string subject, string body);
}

class EmailService: IEmailService {
  public function sendEmail(string from, string to, string subject, string body){
    // sends email over network...
  }
}
```

</v-click>

---

# Writing Testable code (continued...)

> All problems in computer science can be solved by adding another level of indirection.
>
> -- <cite>David Wheeler</cite>

```csharp {all|3-7|15-18|all}
class RegistrationService {

  private IEmailService _emailService;

  public RegistrationService(IEmailService emailService){
    this._emailService = emailService;
  }

  public void register(string username, string email, string password){
    // logic to create user in database
    _emailService.sendEmail("team@website.com", email, "Welcome onboard", "We are happy to have you onboard")
  }
}

// in entry point
IEmailService emailService = new EmailService();
var registrationService = new RegistrationService(emailService);
registrationService.register("developer", "dummyemail@gmail.com", "hashedpassword");
```


---

# Test Doubles



---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---

# Code

Use code snippets and get the highlighting directly![^1]

```ts{all|2|1-6|9|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = {...user, ...update}  
  saveUser(id, newUser)
}
```

<arrow v-click="3" x1="400" y1="420" x2="230" y2="330" color="#564" width="3" arrowSize="1" />

---

# Further Reading


---

# Resources

- https://martinfowler.com/testing/
