---
layout: post
title:      "Final_Project"
date:       2020-11-06 05:05:14 +0000
permalink:  final_project
---


It has been an incredible ride and here we are at the Final project to combine everything that I've learned and put it into something useable. It was really interesting learning about writing in ES6 and how React worked with front end. It was really neat to see how the whole thing comes through, for example how creating the Rails API creats objects and how that can be passed back to the front end to be visually seen on the webpage browser. I really loved learning a lot about how we can just write components and containers and it really made sense to me how this would simplify many things so we can avoid mistakes and a bunch of code just written into one document. I would have to say I would really like to learn more about styling and writing CSS code to firm up how my applications would look as that would really help the presentation. I think I have learned a lot about the actions like onClick and how to handle submit and handle change. Those were interesting concepts and how to handle promises. 

So first off we learned about the components. Components could be classes, or functions and they could have state or be stateless. They could also just be containers where other relevant components could go in to be rendered on to the webpage. I enjoyed learning about setting and then changing the states of components. For example in my code. 
```
class BobaInput extends React.Component {

    state = {
        name: 'Black Sugar Milk Tea',
        quantity: ''
    }

    handleChange = (event) => {
        this.setState({
            [event.target.name]: event.target.value
        })
    }

    handleSubmit = (event) => {
        event.preventDefault()
        this.props.addBoba(this.state, this.props.account.id)
        this.setState(
            {
                name: '',
                quantity: ''
            }
        )
    }


    render () {
        return(
            <div>
                <form onSubmit={this.handleSubmit}>
                    <label>Boba Name:</label>
                    <select name='name' value={this.state.name} onChange={this.handleChange}> 
                        <option>Black Sugar Milk Tea</option>
                        <option>Regular Milk Tea</option>
                        <option>Taro Milk Tea</option>
                        <option>Thai Iced Tea</option>
                    </select>
                    <label>Quantity:</label>
                    <input type='text' name='quantity' value={this.state.quantity} onChange={this.handleChange}/> 
                    <input type='submit'/>
                </form>
            </div>
        )
    }

}
```
I first set a state to default. In my form an user is allowed to select the drink and the quantity. This would then changed the state after as you are entering these in through the handle change function, because in there there is a setState function that changes the state to the target.value. After we click submit the state then is passed on to addBoba which is an action and in that action the state is feeding the name and quantity of boba that we had selected back to the backend. In the backend it is where I wrote the logic to only create an order if we have a name of the boba and the quantity. So now that the params satisfies both conditions it will create the order and based off which account sent that order in it will calculate the cost and subtract it from the balance. If we delete the order it will do the opposite. The code is where I expressed the logic. 
```
    def update_balance(boba)
        self.balance = self.balance - boba.quantity*5
        if  self.balance >= 0
            self.save
        else 
            return "Balance too low!"
        end 
    end 

    def update_balance_on_delete(boba)
        self.balance = self.balance + boba.quantity*5
        self.save
    end 
```

There also is a lot of stateless components that could be created that would just get rid of a lot of clutter while programming. For example I created an image file that contained all the images of bobas that I wanted to portray and named it there and then imported that in to my show page to show the user. However they were two different files, that way I just need to change the url on the image file and not search through my whole entire show page file to search for the image url if I wanted to change it. Below is the code of the example I'm talking about. 
```
import React from 'react'

const BobaImages = () => {

    return (
        <div>
            <img src="https://images.summitmedia-digital.com/spotph/images/2019/01/16/brownsugarmilktea-640-1547636407.jpg" alt = '' height={200} width={200} /> Black Sugar Milk Tea
            <br></br> <br></br>
            <img src="https://www.thestar.com/content/dam/thestar/life/food_wine/2017/07/26/is-chatimes-milk-tea-too-sweet-for-a-regular-treat-the-dish/chatime.jpg" alt = '' height={200} width={200} /> Regular Milk Tea
            <br></br> <br></br>
            <img src="https://static.onecms.io/wp-content/uploads/sites/9/2016/04/taro-bubble-tea-XL-RECIPE0316.jpg" alt = '' height={200} width={200} /> Taro Milk Tea
            <br></br> <br></br>
            <img src="https://img.buzzfeed.com/thumbnailer-prod-us-east-1/bd83cc37334e44fda6ed27654fdbd897/BFV41761_DeliciousAsianDrinks_FBFINAL_v5.jpg" alt = '' height={200} width={200} /> Thai Iced Tea
            <br></br> <br></br>
        </div>
    )
}

export default BobaImages
```
```
import React from 'react';
import BobasContainer from '../containers/BobasContainer'
import BobaImages from '../components/BobaImages'


const AccountShow = (props) => {

    let account = props.accounts.filter(account => account.id === parseInt(props.match.params.id))[0]

    return (
        <div>
            <h1>Current Account and Balance</h1>
            <h2>
                {account ? account.name : null} - {account ? account.balance : null}
            </h2>
            <BobasContainer account={account}/>
            <h1>Menu</h1> <br></br>
            <BobaImages />
        </div>
    )


}

export default AccountShow
```

One thing we also learned was routes. I personally think that it made things a lot easier where we would just see it in our files where things were going and we can tell it the exact path that it has to hit for it be there. For example, in the snippet below, the url has to be our server homepage for it to render the component Welcome. 
```
render() {
    return (
      <div className="App">
        <Navbar/>
        <Switch>   
          <Route exact path="/" component={Welcome}/>
        </Switch>
        <AccountsContainer/>
      </div>
    );
  }
```
```
render () {
        return (
            <div>
                <Switch>
                    <Route path='/accounts/new' component={AccountInput}/>
                    <Route path='/accounts/:id' render={(routerProps) => <AccountShow {...routerProps} accounts={this.props.accounts}/> }/>
                    <Route path='/accounts' render={(routerProps) => <Accounts {...routerProps} accounts={this.props.accounts}/> }/>
                </Switch>
            </div>
        )
    }
```
However we also have this route path in my account container that passes in props for us to use when we hit that component. This is something that I found very fascinating on how information were passed from one webpage to another. 

As mentioned before one of the most important learnings throughout this project I had was state and props. How one component can have a state and how that could be passed in as props to another component. That eases up a lot of my programming because I can send information between different webpages and not have to worry how to pass down the information. This project really taught me a lot of the capability built in react, redux, react-dom. I had tons of learnings and fun with this project and I'm really excited to be out there in the real world to look at how things are actually ran! In conclusion, this project intensified my feeling on the satisfaction I get out of progamming something from 0 and built out something that could be actually used in real life, although not perfect yet. This accomplishment was one of the best things i've experienced and I hope I get to have more of these sense of accomplishments in the future. 
