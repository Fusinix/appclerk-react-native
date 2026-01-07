<p align="center">
  <img src="https://appclerk.dev/images/logo-main.png" alt="AppClerk Core Banner" width="300" />
</p>

# appclerk-react-native

React Native SDK for AppClerk - React Native/Expo components and hooks for compliance infrastructure.

## Installation

### React Native (Bare Workflow)

```bash
npm install appclerk-core appclerk-react-native react-native-markdown-display react-native-webview
# or
yarn add appclerk-core appclerk-react-native react-native-markdown-display react-native-webview
```

### Expo

```bash
npx expo install appclerk-core appclerk-react-native react-native-markdown-display react-native-webview
# or
npm install appclerk-core appclerk-react-native react-native-markdown-display react-native-webview
```

## Usage

### Setup Provider

```tsx
// App.tsx (React Native bare workflow)
import { AppClerkProvider } from 'appclerk-react-native';

export default function App() {
  return (
    <AppClerkProvider
      apiKey={process.env.APPCLERK_API_KEY}
      projectId={process.env.APPCLERK_PROJECT_ID}
    >
      <YourApp />
    </AppClerkProvider>
  );
}
```

```tsx
// App.tsx (Expo)
import { AppClerkProvider } from 'appclerk-react-native';

export default function App() {
  return (
    <AppClerkProvider
      apiKey={process.env.EXPO_PUBLIC_APPCLERK_API_KEY}
      projectId={process.env.EXPO_PUBLIC_APPCLERK_PROJECT_ID}
    >
      <YourApp />
    </AppClerkProvider>
  );
}
```

### Components

#### Privacy Policy

```tsx
import { PrivacyPolicy } from 'appclerk-react-native';
import { View } from 'react-native';

export function SettingsScreen() {
  return (
    <View>
      <PrivacyPolicy
        renderMode="native"
        displayMode="inline"
      />
    </View>
  );
}
```

#### Terms of Service

```tsx
import { TermsOfService } from 'appclerk-react-native';
import { View } from 'react-native';

export function SettingsScreen() {
  return (
    <View>
      <TermsOfService
        renderMode="native"
        displayMode="modal"
      />
    </View>
  );
}
```

#### Compliance Badge

```tsx
import { ComplianceBadge } from 'appclerk-react-native';
import { View } from 'react-native';

export function OnboardingScreen() {
  return (
    <View>
      <ComplianceBadge
        style="compact"
        showLink={true}
      />
    </View>
  );
}
```

### Hooks

#### useDocumentContent

```tsx
import { useDocumentContent } from 'appclerk-react-native';
import { View, Text } from 'react-native';

function MyComponent() {
  const { data, loading, error } = useDocumentContent({
    documentType: 'privacy-policy',
  });

  if (loading) return <Text>Loading...</Text>;
  if (error) return <Text>Error: {error.message}</Text>;

  return <Text>{data?.content}</Text>;
}
```

#### useComplianceStatus

```tsx
import { useComplianceStatus } from 'appclerk-react-native';
import { View, Text } from 'react-native';

function MyComponent() {
  const { data, loading } = useComplianceStatus({
    refreshInterval: 60000, // Refresh every minute
  });

  if (loading) return <Text>Loading...</Text>;

  return <Text>Score: {data?.score}%</Text>;
}
```

## API Reference

### Components

- `<AppClerkProvider />` - Context provider (required)
- `<PrivacyPolicy />` - Privacy policy document viewer
- `<TermsOfService />` - Terms of service document viewer
- `<ComplianceBadge />` - Compliance verification badge
- `<ComplianceStatus />` - Detailed compliance status display

### Hooks

- `useAppClerk()` - Access AppClerk instance
- `useDocumentContent()` - Fetch document markdown
- `useDocumentMetadata()` - Fetch document metadata
- `useComplianceStatus()` - Fetch compliance status

## Rendering Modes

### Native Mode (Default)

Renders markdown natively using `react-native-markdown-display`:

- Better performance
- Native feel
- Better offline support
- Full styling control

### Webview Mode

Loads hosted HTML in a WebView:

- Exact rendering match
- Zero styling needed
- Always up-to-date
- Simpler implementation

## Expo Compatibility

This package is fully compatible with Expo and works in both:
- Expo Go (for development)
- EAS Build (for production)

Use `EXPO_PUBLIC_` prefix for environment variables in Expo projects.

## License

MIT

Official documentation: https://appclerk.dev/docs/sdk/react-native

Appclerk Core: https://appclerk.dev/docs/sdk/core

Appclerk React: https://appclerk.dev/docs/sdk/react
