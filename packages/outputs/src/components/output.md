The `<Output />` element is a glorified Switch statement for picking what to render an output with.

```jsx
// Until we create <Stream />
const StreamText = require("./stream-text").default;

const output = Object.freeze({
  outputType: "stream",
  text: "Hello World\nHow are you?",
  name: "stdout"
});

<Output output={output}>
  <StreamText />
</Output>;
```

```jsx
const { RichMedia } = require("./rich-media");

const StreamText = require("./stream-text").default;

// Some "rich" handlers for Media
const Plain = props => <marquee>{props.data}</marquee>;
Plain.defaultProps = {
  mediaType: "text/plain"
};

const HTML = props => <div dangerouslySetInnerHTML={{ __html: props.data }} />;
HTML.defaultProps = {
  mediaType: "text/html"
};

const DisplayData = props => (
  <RichMedia data={props.data} metadata={props.metadata}>
    {props.children}
  </RichMedia>
);

DisplayData.defaultProps = {
  outputType: "display_data"
};

const outputs = [
  {
    outputType: "stream",
    text: "Hello World\nHow are you?",
    name: "stdout"
  },
  {
    outputType: "display_data",
    data: {
      "text/plain": "O____O"
    },
    metadata: {}
  },
  {
    outputType: "stream",
    text: "Pretty good I would say",
    name: "stdout"
  }
];

<div>
  {outputs.map(output => (
    <Output output={output}>
      <StreamText />
      <DisplayData>
        <Plain />
        <HTML />
      </DisplayData>
    </Output>
  ))}
</div>;
```
