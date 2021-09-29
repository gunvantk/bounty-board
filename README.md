# DAO Bounty Board

[![Netlify Status](https://api.netlify.com/api/v1/badges/8e12fc34-94a3-4c7a-8323-fc2b7e1d4d14/deploy-status)](https://app.netlify.com/sites/bounty-board-29081e/deploys)

Project Page:
https://www.notion.so/bankless/Bounty-Board-318dc164cc5640cca17e0fb5f484fd90

### Specifications:

- [Specs page](https://docs.google.com/document/d/1VJXin9Uoqt54JjfQEtyM11XESb2l4C1SSAzgc0kvxIs/edit?usp=sharing)
- [Figma](https://www.figma.com/file/venmq7OWr8iRsjR9ecttvc/Untitled?node-id=1%3A7)
- [Whimsical](https://whimsical.com/bounty-board-design-bankless-2cPEEZinYKJ2zE2Zvq7iAZ)
- [Heroku](https://bounty-board.herokuapp.com/)
- [Possible Queries](https://www.notion.so/Bounty-Board-Queries-33d03a4330454e67b8194aa86274ec34)
- [Data Fields](https://docs.google.com/document/d/10jgHxEpkPlArGlsQH1g22utFrAFh2lK-fbXjbq8KkuU/edit)
- [Personas](https://www.notion.so/Bounty-Board-Personas-8e8f2789775a445c82d13c2a9c545185)
- [Bot flowchart](https://media.discordapp.net/attachments/852736763205910538/857786834682511370/image0.jpg?width=978&height=683)

# Project Overview

## Problem

Currently, Bankless DAO bounties are not in a centralized location causing confusion and makes it challenging for members, new and old, to contribute. Also Level 0's do not have intuitive ways to get involved and earn $BANK other than buying in the secondary markets.

## Solution

For the DAO to grow, we need a way to attract, retain and coordinate talent. The bounty board, accessible to members and non-members will connect the DAO to a continually expanding talent pool.

In addition, we need a way to codify meaningful units of work. Given the diversity of jobs to be done in a DAO, the bounty board allows bounty _creators_ to define and specify the scope of tasks along with expected deliverables.

Finally, we need a way to formalize the flow of capital, beyond an informal, organic tipping culture that exists to formally recognize contributors for their knowledge, skills and abilities.

The bounty board will be a key mechanism for coordinating talent, tasks and capital.

## Minimal Viable Product 1.0

### Bounty Card Definition

For the MVP, we are focusing on the bare requirements for a Bounty Card to be created by a user via DEGEN and/or Frontend UI, with the following key fields:

- **Title**: Bounty Titles should be like headlines
- **Description**: Provides space to flesh out the scope, deliverables and timeline for the bounty.
- **Criteria**: When is a task considered "done" or "complete"?
- **Reward**: Bounty creator indicates `amount` (i.e., 10000) and `currency` (i.e., $BANK) to be paid for completing the work.
- **HashId**: Auto-generated ID for each bounty.
- **CreatedBy / RequestedBy**: Bot automatically enters bounty creator's `discordHandle`.
- **ClaimedBy**: Bot automatially notes `discordHandle` claiming the bounty.
- **SubmittedBy**: Bot automatically notes `discordHandle` submitting the bounty.

#### User Experience Discord: Creating a Bounty with DEGEN

The follow description is of Serendipity in the Bankless Bot Garage, but is intended to mirror how DEGEN works in production.

1. **Create**: Bounty creator creates new bounty with `/bounty create`, inputing `title` and `reward`. DEGEN will dm you to input a description, requirements for completion and a due date (`yyyy-mm-dd`). DEGEN takes your input and returns a card with three options: 👍 publish, 📝 edit or ❌ delete

1. **Create Multiple Bounties**: Bounty creator creates new bounty with `/bounty create`, inputing `title` and `reward`. Then, hit tab to see an optional `copies` feature to create multiple bounties at once.

1. **Edit**: Select 📝 to edit. DEGEN provides a link to the frontend to edit any field. DEGEN then re-shows a newly edited card (and automatically publishes to #🧀-bounty-board channel)
1. **Publish/Open**: Bounty creator clicks thumbs up emoji 👍 or `/bounty publish` in Discord, bounty published to #🧀-bounty-board channel and website (url provided); status is now _Open_ on website.
1. **Claim/In Progress**: Within #🧀-bounty-board Bounty _claimer_ click black flag 🏴 or `/bounty claim`, entering the `HashID` to 'start', card changes color in Discord, Bounty creator receives message that bounty has been claimed; Bounty card on website now has _Claimed By_; card status is now "In Progress".
1. **Submit/In Review**: Bounty claimer hits red mail box emoji 📮 in Discord, receives auto-generated message from DEGEN notifying the bounty is ready for review. They should reach out to the person who submitted the bounty. Alternatively, user can submit directly through a new bot command `/bounty submit`, entering `HashId`; card status is now "In Review".
1. **Complete/Completed**: Bounty claimer can signal completion ✅ on the post in the #🧀-bounty-board channel or directly through a new bot command `/bounty complete true`; card status is now "Completed".

#### Degen Commands

1. **NOTE**: DEGEN is available for use on _any_ channel within the Bankless DAO discord (08/31/2021)
2. Enter `/` and see a list of commands pop up.

The following commands (and input fields) are available for DEGEN:

/bounty claim (bounty-id)
/bounty complete (bounty-id)
/bounty create (title)(reward)
/bounty publish (bounty-id)
/bounty list (list-type)
/bounty delete (bounty-id)
/bounty submit (bounty-id)
/help bounty

Refer to the [Bounty Board Commands and Workflow](https://bankless.notion.site/The-Bounty-Board-Commands-and-Workflow-7f15bbc3f2c744afab1cb5f90daac4a2) Notion Page for in-depth details.

#### User Experience Frontend: Claiming a Bounty

**Note**: Currently, the frontend mirrors the interaction with DEGEN in discord and displays changes in card status. Frontend interactions are suited for those wishing to _claim_ bounties.

1. **Claim**: Click on any card that says `Open`. To claim, click the `Claim it` button. You will be re-directed to #🧀-bounty-board channel. Within #🧀-bounty-board Bounty click black flag 🏴 emoji. DEGEN present a link _back_ to the frontend and a prompt to reach out to the Bounty Creator.

2. **Frontend Status: In Progress**: A link back to the frontend shows card status as "In Progress" and "Claimed By" claimer's discord handle.

3. **Discord/Bot: Submit**: Bounty claimer hits red mail box emoji 📮 in Discord to submit, receives auto-generated message from DEGEN indicating "bounty in review" and a link back to the frontend where status is now "In Review".

4. **Discord/Bot: Complete**: Bounty claimer can signal completion ✅ on the post in the #🧀-bounty-board channel. Bounty creator receives message to tip bounty completer.

5. **Frontend Status: Completed**: Back at the frontend, the bounty card status is now "Completed".
