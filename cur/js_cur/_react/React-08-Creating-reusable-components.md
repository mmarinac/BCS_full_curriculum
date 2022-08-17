# React 08: Creating reusable components

---

<details>
    <summary>🎬 Video: React -- reusable components</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/imCLGesg9Xk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

The beauty of react is that if done properly components are reusable, although the concept could be overwhelming at first is actually one of the strongest points of react.

Let’s take for example a message component, we could use this component to display messages, for example when the user signed in, or when the password they entered was wrong.

Now we could simply hardcode our message, however if we do that we would have to rewrite a message component every time which isn’t great.

So ideally we would have a message component that can change message, color and also be visible or not depending on our app state.


<iframe src="https://codesandbox.io/embed/eloquent-villani-4ggrl?fontsize=14" title="React Block 8- 1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

Now the above component background color, header message and body message are all dependent from the props it receives from its parent component.

Also if the state display is set to none then it will not be displayed at all.
so we can have the message always there but not being displayed unless we change the state of our application to block.

Let’s say for example our user try logging in but he enters a wrong password so what we should do is state the state accordingly and then pass it through props.

<iframe src="https://codesandbox.io/embed/react-block-8-2-p8w2s" title="React Block 8 -2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

Another example of reusable component could be a responsive container which has all the styles and rendering children inside via props. In the following codesandbox we have a component Grid which can render children in a given number columns passed via props. In this case any moment we need to create a Grid container we simply import and wrap it around the content.

<iframe
     src="https://codesandbox.io/embed/reusable-grid-component-9i124?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="reusable grid component"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

