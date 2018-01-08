---
layout: post
title: "React Study[1]: basic"
date: "2017-11-15 09:54:42 -0800"
location: "San Diego, CA"
commentIssueId: 25
category: React
tags: [react, web, study, ui, library]
---
**React study posts are my study logs of [Nomad coders : ReactJS fundamentals](https://academy.nomadcoders.co/p/reactjs-fundamentals)**

[React](https://reactjs.org/) is developed by Facebook Inc. It's highly growing and most loved library by web developers.

- React is not a framework.
React is an UI library which will help you out to make all the stuffs of web design easier. And that means you can work on Front-end side with full of react and use any framework you like to use, Django, ruby on rails, flask, etc.

- React uses JSX
[JSX](https://jsx.github.io/)([React : JSX in depth](https://reactjs.org/docs/jsx-in-depth.html)) is extended language of JavaScript. It's faster, type-safe and easy to code, they said.. :)
{% highlight text %}
JSX is a statically-typed, object-oriented programming language designed to run on modern web browsers. Being developed at DeNA as a research project, the language has following characteristics.
{% endhighlight %}

- React is component based.
All things you can make with react are components. You build a component and make a CSS for the component and just use it! Every components has their own state and it's handled by engine. So you don't have to worry about saving or writing new data or do extra stuffs to handle all data. Build component and attach it.

  Component has props(property). Parent component can give properties to child component and they can be updated really easily.
{% highlight javascript %}
class Movie extends Component {
  render() {
    return (
      <Hello title={"hello"}/>
    );
  }
}


Movie is just sending hello string value to Hello class
{% endhighlight %}


{% highlight javascript %}
class Hello extends Component {
  render() {
    return (
      <div> {this.props.title} </div>
    );
  }
}


child component can use this.props.title
{% endhighlight %}

- ReactDOM and React-native
ReactDOM(Document object model) is for web application and react-native is for mobile application.

- PropTypes
React.propTypes is deprecated thus you can install PropTypes from yarn or npm and import it to keep using it fancy.
{% highlight bash %}
yarn add PropTypes

or

npm install --save PropTypes
{% endhighlight %}

{% highlight javascript %}
import PropTypes from 'prop-types';

and at the top of the class,

static propTypes = {
  name:PropTypes.string.isRequired,
  key:PropTypes.number.isRequired
}
{% endhighlight %}
