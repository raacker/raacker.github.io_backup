---
layout: post
title: "React Study [3] : Lifecycle"
date: "2017-11-15 11:31:40 -0800"
location: "San Diego, CA"
commentIssueId: 27
category: React
tags: [react, web, study, ui, library]
---
There is two type of life cycle of components. You can check out the [official document](https://reactjs.org/docs/react-component.html) too.

<h2>Rendering (Mounting)</h2>

To create components on your website, components must be rendered. We also call it mounting.

{% highlight text %}
constructor() -> componentWillMount() -> render() -> componentDidMount()
{% endhighlight %}

They are inherited from Component class so you can put console.log to check how they are called.

- **constructor()**

  As we know, constructor is a blue-print for class. So constructor should call super(props) at the first to call parent's constructor.
  In the constructor, you can initialize state of component or bind methods.

  You should aware of changing state with constructor. There is a good way to manage state. [Lifting state up](https://reactjs.org/docs/lifting-state-up.html)

- **componentWillMount()**

  It's like receiving request from client or somewhere. This method is saying this component will call render method soon.

- **render()**

  component is created from constructor and it's ready to be drawn on web

- **componentDidMount()**

  Every process was successful and you can see component on your html page. Thus, it is best place to call **network request** and gather data from server. And also good for subscription.



<h2>Updating</h2>

I think the most coolest thing of react is how it renders the components. And that's why react is easy to use and easy to manipulate.

{% highlight text %}
componentWillReceiveProps() -> shouldComponentUpdate() -> componentWillUpdate() -> render() -> componentDidUpdate()
{% endhighlight %}

- **componentWillReceiveProps(nextProps)**

  You will be able to check this.props and nextProps to check if the component needs to be updated and change the state calling this.setState().
  It will not called during mounting.

- **shouldComponentUpdate(nextProps, nextState)**

  It is invoked before rendering when new props or state are being received. Remember, componentWillReceiveProps() is called before the component received new props and shouldComponentUpdate() is called when component is receiving new props or state. Thus, to update component, shouldComponentUpdate() must be called.

- **componentWillUpdate(nextProps, nextState)**

  This method will be invoked to prepare the update. For example, show waiting gif image to indicate user it is updating right now.

- **render()**

  during the update, render is invoked again.

- **componentDidUpdate(prevProps, prevState)**

  Indicating component is updated successfully. So you can request network service or do anything you need to.
