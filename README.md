# Lido Validator Exit Notification Setup

This project sets up a Tenderly Web3 Action to monitor Lido validator exit requests and send notifications via Telegram when specific conditions are met.

## Prerequisites

- [Tenderly CLI](https://github.com/Tenderly/tenderly-cli)
- [Node.js](https://nodejs.org/) (version 16 or higher)
- [npm](https://www.npmjs.com/)
- A Telegram bot token and channel ID
- A Tenderly account and project

## Setup

1. Clone this repository:
   ```
   git clone <repository-url>
   cd <repository-name>
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Set up your Tenderly project:
    - Log in to your Tenderly account
    - Create a new project or use an existing one
    - Note down your `Account Name` and `Project Slug`

4. Configure your `tenderly.yaml` file:
    - Replace the `<YOUR_ACCOUNT_ID>` and `<YOUR_PROJECT_SLUG>` fields with your Tenderly `Account Name` and `Project Slug`
    - Ensure the `action_name` matches the name you want to use for your Web3 Action

5. Set up your secrets in Tenderly:
    - Go to your Tenderly project settings
    - Add the following secrets:
        - `BEARER`: Your Tenderly API bearer token
        - `BOT-TOKEN`: Your Telegram bot token
        - `CHANNEL-ID`: Your Telegram channel ID

## Deployment

To deploy the Web3 Action, use the Tenderly CLI:

```
tenderly actions deploy
```

This command will deploy the action defined in your `tenderly.yaml` file.

## How it Works

The Web3 Action (`lidoEvents.ts`) does the following:

1. Listens for `ValidatorExitRequest` events from the Lido contract on the Ethereum mainnet.
2. When an event is detected, it retrieves the transaction details using the Tenderly API.
3. It checks if the `stakingModuleId` is 1 and the `nodeOperatorId` is 14.
4. If the condition is met, it sends a notification to the specified Telegram channel with details about the validator exit request.

## Customization

To modify the conditions or add more events to monitor:

1. Edit the `lidoEvents.ts` file.
2. Update the condition check in the `if` statement to match your requirements.
3. Modify the message format or add additional information as needed.

## Monitoring and Troubleshooting

- You can monitor your Web3 Action executions in the Tenderly dashboard.
- Check the Tenderly logs for any error messages or execution details.
- Ensure your Telegram bot has permission to send messages to the specified channel.

## Important Notes

- This setup is specifically designed to monitor Lido validator exit requests on the Ethereum mainnet.
- The current configuration filters for `stakingModuleId: 1` and `nodeOperatorId: 14`. Adjust these values as needed for your use case.
- Ensure you have sufficient credits in your Tenderly account to run the Web3 Action.

## Additional Resources

- [Tenderly Web3 Actions Documentation](https://docs.tenderly.co/web3-actions/intro-to-web3-actions)
- [Telegram Bot API Documentation](https://core.telegram.org/bots/api)

For more information on Lido staking and node operator responsibilities, refer to the [Lido documentation](https://docs.lido.fi/staking-modules/csm/guides/events).
