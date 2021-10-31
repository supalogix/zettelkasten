https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub

Foreword
There are several definitions of objects, that are not real. The general term is test double. This term encompasses: dummy, fake, stub, mock.

Reference
According to Martin Fowler's article:

Dummy objects are passed around but never actually used. Usually they are just used to fill parameter lists.
Fake objects actually have working implementations, but usually take some shortcut which makes them not suitable for production (an in memory database is a good example).
Stubs provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test. Stubs may also record information about calls, such as an email gateway stub that remembers the messages it 'sent', or maybe only how many messages it 'sent'.
Mocks are what we are talking about here: objects pre-programmed with expectations which form a specification of the calls they are expected to receive.
Style
Mocks vs Stubs = Behavioral testing vs State testing

Principle
According to the principle of Test only one thing per test, there may be several stubs in one test, but generally there is only one mock.

Lifecycle
Test lifecycle with stubs:

Setup - Prepare object that is being tested and its stubs collaborators.
Exercise - Test the functionality.
Verify state - Use asserts to check object's state.
Teardown - Clean up resources.
Test lifecycle with mocks:

Setup data - Prepare object that is being tested.
Setup expectations - Prepare expectations in mock that is being used by primary object.
Exercise - Test the functionality.
Verify expectations - Verify that correct methods has been invoked in mock.
Verify state - Use asserts to check object's state.
Teardown - Clean up resources.
Summary
Both mocks and stubs testing give an answer for the question: What is the result?

Testing with mocks are also interested in: How the result has been achieved?


https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub

Stub

I believe the biggest distinction is that a stub you have already written with predetermined behavior. So you would have a class that implements the dependency (abstract class or interface most likely) you are faking for testing purposes and the methods would just be stubbed out with set responses. They would not do anything fancy and you would have already written the stubbed code for it outside of your test.

Mock

A mock is something that as part of your test you have to setup with your expectations. A mock is not setup in a predetermined way so you have code that does it in your test. Mocks in a way are determined at runtime since the code that sets the expectations has to run before they do anything.

Difference between Mocks and Stubs

Tests written with mocks usually follow an initialize -> set expectations -> exercise -> verify pattern to testing. While the pre-written stub would follow an initialize -> exercise -> verify.

Similarity between Mocks and Stubs

The purpose of both is to eliminate testing all the dependencies of a class or function so your tests are more focused and simpler in what they are trying to prove.





https://testing-library.com/docs/react-testing-library/example-intro


// __tests__/fetch.test.js
import React from 'react'
import {rest} from 'msw'
import {setupServer} from 'msw/node'
import {render, fireEvent, waitFor, screen} from '@testing-library/react'
import '@testing-library/jest-dom'
import Fetch from '../fetch'

const server = setupServer(
  rest.get('/greeting', (req, res, ctx) => {
    return res(ctx.json({greeting: 'hello there'}))
  }),
)

beforeAll(() => server.listen())
afterEach(() => server.resetHandlers())
afterAll(() => server.close())

test('loads and displays greeting', async () => {
  render(<Fetch url="/greeting" />)

  fireEvent.click(screen.getByText('Load Greeting'))

  await waitFor(() => screen.getByRole('heading'))

  expect(screen.getByRole('heading')).toHaveTextContent('hello there')
  expect(screen.getByRole('button')).toBeDisabled()
})

test('handles server error', async () => {
  server.use(
    rest.get('/greeting', (req, res, ctx) => {
      return res(ctx.status(500))
    }),
  )

  render(<Fetch url="/greeting" />)

  fireEvent.click(screen.getByText('Load Greeting'))

  await waitFor(() => screen.getByRole('alert'))

  expect(screen.getByRole('alert')).toHaveTextContent('Oops, failed to fetch!')
  expect(screen.getByRole('button')).not.toBeDisabled()
})



https://www.telerik.com/products/mocking/unit-testing.aspx#:~:text=Mocking%20frameworks%20are%20used%20to,substitutes%20for%20unit%20testing%20frameworks.


What is mocking?
Mocking is a process used in unit testing when the unit being tested has external dependencies. The purpose of mocking is to isolate and focus on the code being tested and not on the behavior or state of external dependencies. In mocking, the dependencies are replaced by closely controlled replacements objects that simulate the behavior of the real ones. There are three main possible types of replacement objects - fakes, stubs and mocks.

Fakes: A Fake is an object that will replace the actual code by implementing the same interface but without interacting with other objects. Usually the Fake is hard-coded to return fixed results. To test for different use cases, a lot of Fakes must be introduced. The problem introduced by using Fakes is that when an interface has been modified, all fakes implementing this interface should be modified as well.

Stubs: A Stub is an object that will return a specific result based on a specific set of inputs and usually won’t respond to anything outside of what is programed for the test. With JustMock you can create a Stub in a test with a minimal amount of code, making it clear how the dependency will respond and how the tested system should behave.

Mocks: A Mock is a much more sophisticated version of a Stub. It will still return values like a Stub, but it can also be programmed with expectations in terms of how many times each method should be called, in which order and with what data. With JustMock you can create a Mock with just one line of code, which makes the test more understandable.



What is a mocking framework?
Mocking frameworks are used to generate replacement objects like Stubs and Mocks. Mocking frameworks complement unit testing frameworks by isolating dependencies but are not substitutes for unit testing frameworks. By isolating the dependencies, they help the unit testing process and aid developers in writing more focused and concise unit tests. The tests also perform faster by truly isolating the system under test.
