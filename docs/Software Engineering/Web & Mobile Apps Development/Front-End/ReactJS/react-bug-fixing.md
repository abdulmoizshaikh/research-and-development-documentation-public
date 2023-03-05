# React Errors and solutions

**67:7 error Visible, non-interactive elements with click handlers must have at least one keyboard listener jsx-a11y/click-events-have-key-events**

Add this line into your component

```jsx showLineNumbers
onKeyDown={() => setSelectedCard(payload)}

//Like

<div
className={classes.card_list}
onClick={() => setSelectedCard(payload)}
onKeyDown={() => setSelectedCard(payload)}
>
```

**67:7 error Static HTML elements with event handlers require a role jsx-a11y/no-static-element-interactions**

Add this line into your component

```jsx showLineNumbers
aria-hidden='true'

//Like

<div
aria-hidden='true'
className={classes.card_list}
onClick={() => setSelectedCard(payload)}
onKeyDown={() => setSelectedCard(payload)}
>
```

**How to style placeholders in textfield in material ui.**

Add this line in inputProps

```jsx showLineNumbers
classes: { input: classes.input },

//style.js
input: {
fontWeight: '600',
fontSize: '24px',
textOverflow: 'ellipsis !important',
'&::placeholder': {
color: '#342D3D',
fontWeight: '600',
fontSize: '24px',
},
},
```

```jsx showLineNumbers
e.g
 <TextField
        className={classes.textInput}
        variant="outlined"
        name="salePrice"
        type="number"
        placeholder="0"
        value={topUpAmount}
        onChange={(e) => setTopUpAmount(e.target.value)}
        InputProps={{
          startAdornment: (
            <InputAdornment
              position="start"
              style={{
                marginLeft: "30px",
                marginRight: "5px",
                alignItems: "center",
              }}
            >
              <p style={{ color: "#8C9099" }}>AED</p>
            </InputAdornment>
          ),
          classes: { input: classes.input },
        }}
      />
```

https://stackoverflow.com/questions/47804380/styling-the-placeholder-in-a-textfield
