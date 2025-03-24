# 6744 Repo Management Doc

A quick draft of how I think Mehlville RC's Robot Code Repo's should be handled in the season

> [!IMPORTANT]
> This isn't officially official or anything (yet) so don't yell at me if I'm wrong

# Abstract

This Markdown File will go over how *I* believe Mehlville RC's GitHub Repos are managed at these key points in the season:

- Pre-Comp
- Comp

This does not necesarily reflect what *will* happen, but what *I* believe should happen. This will also include code recomendations for how things are named

# Season Key Points

## Pre-Comp

Pre-Comp is the time before the competition we plan to do

## Comp

Comp is defined as the actual Day/Days of the competition we plan to do

# Code Management

## Branches

### Pre-Comp

- Branches should be named with the prefixes:
  - `f-` for a fix without an issue
  - `i-##-` for fix that has an issue (replace `##` with the issue number)
  - `d-xxxx-` for a derivitive of a branch (replace `xxxx` with the original branch name without the prefix)
  - `e-xxxx-` for extending the functionality of a branch (replace `xxxx` with the original branch name without the prefix)
- Additionally, branches should focus on one topic
- If the objective you are doing can be split up into multiple tasks, do that
  - Ex: Make branches off of branches `f-elevator` --> `d-elevator-tuning`, `d-elevator-controls`
> [!NOTE]
> `d-xxxx` should be used for something that the main developer of a branch is working on, while `e-xxxx` should be used for something a *different* developer wants to add

### Comp

- Branches should be named with the prefixes:
  - `hf-` for a one time hotfix
  - `hfr-` for a reoccuring issue
  - `d-xxxx-` for a derivitive of a branch (replace `xxxx` with the original branch name without the prefix)
  - `e-xxxx-` for extending the functionality of a branch (replace `xxxx` with the original branch name without the prefix)
- Branches should still focus on one topic
  - Ex: `hfr-tuning` is good, but `hf-elevator` is not. Keep things separated and organized if possible
> [!NOTE]
> `d-xxxx` should be used for something that the main developer of a branch is working on, while `e-xxxx` should be used for something a *different* developer wants to add
`
## Development Branch

### Pre-Comp

- Development should be under Standard Rules
  - Restrict creations: Only allow users with bypass permission to create matching refs.
  - Restrict updates: Only allow users with bypass permission to update matching refs.
  - Restrict deletions: Only allow users with bypass permissions to delete matching refs.
  - Require linear history: Prevent merge commits from being pushed to matching refs.
  - Required approvals: The number of approving reviews that are required before a pull request can be merged.
    - The number half the size of the dev team 
  - Block force pushes: Prevent users with push access from force pushing to refs

### Comp

- Development should use less strict or no ruling

## Project Tracking

### Pre-Comp

- GitHub Issues should be used to track issues/features we need to add
  - Make sure to reference a development branch/PR in the issue
- PRs should always remain PR Drafts until tested and ready to ship
- Ideally you should create a PR Draft as soon as you start a branch

### Comp

- GitHub Issues can be used to track issues/features, but are not required during Comp
- PRs should be made as full PRs and be made & merged when tested
- It is advised you make a PR Draft, but is not required
  - If you do make an issue, make sure to reference a development branch/PR in the issue

# Code Naming Conventions

## Variables

All variables for the most part will follow `camelCase` conventions. If a variable is a Constant, it may be preceded by a `k`, which **WILL** affect the `camelCase`. If more context about the Constant is required, use a docstring. If a variable is a Physical Hardware Component, it has a `m_snakeHead`, which means that it will start with a leading letter, then an underscore which **WILL NOT** affect the `camelCase`. The `m_snakeHead` should be indicative of what it represents. `m_` is often used for motors, `p_` is often used for PID, and `e_` is often used for encoders. If you are unsure of what you should choose, just go with `m_` as your default. Any other variables that aren't physical hardware or constants will use `camelCase`.

## Methods

All methods will follow `camelCase` conventions. There isn't any weird trickery with methods, just name them simply. Additionally, put a docstring describing functionality of the method

## Classes

All classes will follow `PascalCase`. Again, no trickery, just name them simply and put a docstring if necesary.

## Example Code

```java
//            Class          Hardware
//            vvvvvvvvvvvvvv vvvvvvvvvvvv
private final DriveSubsystem m_robotDrive = new DriveSubsystem();

//...

// This is a Docstring
// vvvvvvvvvvvvvvvvvvv
/**
 * Sets the swerve ModuleStates.
 *
 * @param desiredStates The desired SwerveModule states.
 */

//          Method                              Variable
//          vvvvvvvvvvvvvvv                     vvvvvvvvvvvvv
public void setModuleStates(SwerveModuleState[] desiredStates) {
  //...
}

//...

//                      Constant
//                      vvvvvvvvvvvvvv
public static final int kShepherdCanId = 7;
```