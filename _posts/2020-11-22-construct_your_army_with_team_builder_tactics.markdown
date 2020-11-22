---
layout: post
title:      "Construct your army with Team Builder Tactics"
date:       2020-11-22 21:15:26 +0000
permalink:  construct_your_army_with_team_builder_tactics
---


In chess, positioning is everything.  Of course, knowing which units to use for which purposes is equally important, but the true strategy of a game like chess is outwitting your opponent through clever placement of your units.  Over a year ago, Riot Games released a completely unique game mode called Team Fight Tactics that took the champions from their wildly popular League of Legends franchise and made them into pawns in a big game of chess.  Each unit has different abilities and stats, and they work together to automatically battle the opponent's army at the start of each round.  As you can imagine, deciding how to position these units-- especially when they move and act on their own-- is often the deciding factor in who wins each round.  For my Javascript Final Project, I decided to create a SPA that mimics the board of hexagons present in TFT and allows a user to place the units and save them to a team.

After working with Javascript over the course of this project, I came to love the cycle of "grab element, change element, push to DOM".  There's something very satisfying about seeing an immediate change to the DOM based off a user's actions.  For instance, I have a function, bindDeleteListeners(), that iterates over all of the items in a list and applies an event listener to each one.  Suddenly I have a dynamic list of items that each have the power to influence the DOM in some way!

```
const listItems = document.querySelectorAll(".list-group-item")
        for (const listItem of listItems) {
            listItem.addEventListener('click', function(e) {
                const deleteBTN = document.getElementById("delete-space")
                deleteBTN.innerHTML += `<button type="delete" name="delete-button" value="Delete" id="${e.target.id}">Delete Board</button>`
```

Fetching boards to render entire teams, constructing new objects from the fetch requests, sending data to the backend to be mutated in some way; all of these actions felt very fluid to me and, what's more, they made sense.  After sending a fetch request to my controller, I was able to dictate what information got sent back to the frontend to be displayed.  For example, my Show page for Boards looks like this:

```
def show
        board = Board.find_by(id: params[:id])
        render json: board.to_json(:include => {
            :board_units => {:except => [:created_at, :updated_at] }
        }, :except => [:description, :created_at, :updated_at])
    end
```

I was able to send back a json response with ONLY the information that I wanted it to have, and excluded all of the "fluff".  An action like this makes sense, and it gives you a level of control that is easy to follow along with.

One part of my project that I struggled with initially was sending a fetch POST request to create a new team called a "Board".  I started out by iterating over the entire array of hexes that represents the default board, and, if a unit was found on one of the hexes (the hex ID had become the unit ID), I pushed it into a separate array.  However, at the same time, I was also pushing the hex position into a separate array.  Next, I sent my fetch POST request to my backend with both of these arrays in addition to the input name.  Within my Board Controller's Create action, I was able to manipulate all of this data to establish the connection between the Board, the Board's Units (the Join table), and each individual Unit. 

```
def create 
        board = Board.find_or_create_by(name: params[:name])
        board_units = params[:elements].map.with_index do |e, index|
            id = e.split('_')[1]
            unit = Unit.find_by(id: id)
            position = params[:hex][index].to_i
            BoardUnit.create(unit_id: unit.id, board_id: board.id, hex: position)
        end
        render json: board_units, except: [:created_at, :updated_at]
    end
```

Once the response makes it back to the frontend, Javascript constructs the new Board Unit objects, and from there renders them to the DOM.

Even after spending countless hours working with Javascript, there are still a few things that I need more practice with.  First of all, scoping is a major consideration in any function.  Oftentimes, I'd find myself unable to access a variable I had previously defined because it was out of scope.  The second area is much like the first: the keyword "This".  "This" is an interesting concept because it refers to whatever instance or object is currently scoped.  For example, in my appContainer class, I could call another method within my fetch request by referring to "this" instance of appContainer as shown below:

```
getBoards() {
        fetch(boards_url)
            .then(resp => resp.json())
            .then(boards => this.renderBoards(boards))
```

These two concepts, Scoping and the "This" keyword, still present the biggest challenge to me moving forward.  I know that with time, I will better understand when to use and how to use each to create better, more dynamic webpages.
