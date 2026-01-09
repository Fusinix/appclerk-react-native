<!-- @format -->

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
import { AppClerkProvider } from "appclerk-react-native";

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
import { AppClerkProvider } from "appclerk-react-native";

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
import { PrivacyPolicy } from "appclerk-react-native";
import { View } from "react-native";

export function SettingsScreen() {
	return (
		<View>
			<PrivacyPolicy renderMode="native" displayMode="inline" />
		</View>
	);
}
```

#### Terms of Service

```tsx
import { TermsOfService } from "appclerk-react-native";
import { View } from "react-native";

export function SettingsScreen() {
	return (
		<View>
			<TermsOfService renderMode="native" displayMode="modal" />
		</View>
	);
}
```

#### Compliance Badge

```tsx
import { ComplianceBadge } from "appclerk-react-native";
import { View } from "react-native";

export function OnboardingScreen() {
	return (
		<View>
			<ComplianceBadge style="compact" showLink={true} />
		</View>
	);
}
```

### Hooks

#### useDocumentContent

```tsx
import { useDocumentContent } from "appclerk-react-native";
import { View, Text } from "react-native";

function MyComponent() {
	const { data, loading, error } = useDocumentContent({
		documentType: "privacy-policy",
	});

	if (loading) return <Text>Loading...</Text>;
	if (error) return <Text>Error: {error.message}</Text>;

	return <Text>{data?.content}</Text>;
}
```

#### useComplianceStatus

```tsx
import { useComplianceStatus } from "appclerk-react-native";
import { View, Text } from "react-native";

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

## Style Guide

AppClerk React Native SDK provides comprehensive styling options for all markdown elements. You can style every aspect of your legal documents using the `customStyles` prop with React Native's `ViewStyle` and `TextStyle` objects.

### Styling Methods

#### 1. Container Styling

Use the `style` prop to style the document container:

```tsx
<TermsOfService
	style={{
		padding: 20,
		backgroundColor: "#ffffff",
		borderRadius: 8,
	}}
/>
```

#### 2. Text Styling

Use the `textStyle` prop to apply base text styles:

```tsx
<TermsOfService
	textStyle={{
		fontSize: 16,
		lineHeight: 24,
		color: "#333333",
		fontFamily: "System",
	}}
/>
```

#### 3. Comprehensive Custom Styles (`customStyles`)

Apply granular styles to all markdown elements using the `customStyles` prop:

```tsx
import { TermsOfService } from "appclerk-react-native";

<TermsOfService
	customStyles={{
		// Container styles
		container: {
			padding: 20,
			backgroundColor: "#ffffff",
		},
		// Body/base text styles
		body: {
			fontSize: 16,
			lineHeight: 24,
			color: "#333333",
		},
		// Headings
		h1: {
			fontSize: 28,
			fontWeight: "bold",
			color: "#1a1a1a",
			marginTop: 24,
			marginBottom: 16,
		},
		h2: {
			fontSize: 24,
			fontWeight: "600",
			color: "#2d2d2d",
			marginTop: 20,
			marginBottom: 12,
		},
		h3: {
			fontSize: 20,
			fontWeight: "600",
			color: "#333333",
			marginTop: 16,
			marginBottom: 10,
		},
		h4: {
			fontSize: 18,
			fontWeight: "600",
			color: "#333333",
			marginTop: 14,
			marginBottom: 8,
		},
		// Paragraphs
		p: {
			fontSize: 16,
			lineHeight: 24,
			color: "#4a4a4a",
			marginBottom: 16,
		},
		// Lists
		ul: {
			marginBottom: 16,
			paddingLeft: 20,
		},
		ol: {
			marginBottom: 16,
			paddingLeft: 20,
		},
		li: {
			fontSize: 16,
			lineHeight: 24,
			color: "#4a4a4a",
			marginBottom: 8,
		},
		// Links
		a: {
			color: "#007AFF",
			textDecorationLine: "underline",
		},
		// Text formatting
		strong: {
			fontWeight: "bold",
			color: "#1a1a1a",
		},
		em: {
			fontStyle: "italic",
			color: "#4a4a4a",
		},
		// Code
		code: {
			backgroundColor: "#f3f4f6",
			paddingHorizontal: 6,
			paddingVertical: 2,
			borderRadius: 4,
			fontSize: 14,
			fontFamily: "monospace",
			color: "#1f2937",
		},
		pre: {
			backgroundColor: "#1f2937",
			padding: 12,
			borderRadius: 8,
			marginBottom: 16,
		},
		// Blockquote
		blockquote: {
			borderLeftWidth: 4,
			borderLeftColor: "#3b82f6",
			paddingLeft: 16,
			marginLeft: 0,
			fontStyle: "italic",
			color: "#6b7280",
		},
		// Horizontal rule
		hr: {
			borderTopWidth: 1,
			borderTopColor: "#e5e7eb",
			marginVertical: 24,
		},
		// Tables
		table: {
			width: "100%",
			marginBottom: 16,
		},
		thead: {
			backgroundColor: "#f9fafb",
		},
		tbody: {},
		tr: {},
		th: {
			padding: 12,
			borderWidth: 1,
			borderColor: "#e5e7eb",
			fontWeight: "600",
			fontSize: 14,
		},
		td: {
			padding: 12,
			borderWidth: 1,
			borderColor: "#e5e7eb",
			fontSize: 14,
		},
		// Alternative keys (for react-native-markdown-display compatibility)
		heading1: {
			fontSize: 28,
			fontWeight: "bold",
			marginTop: 24,
			marginBottom: 16,
		},
		heading2: {
			fontSize: 24,
			fontWeight: "600",
			marginTop: 20,
			marginBottom: 12,
		},
		heading3: {
			fontSize: 20,
			fontWeight: "600",
			marginTop: 16,
			marginBottom: 10,
		},
		bullet_list: {
			marginBottom: 16,
		},
		ordered_list: {
			marginBottom: 16,
		},
		listItem: {
			marginBottom: 8,
		},
		paragraph: {
			marginBottom: 16,
			lineHeight: 24,
		},
		text: {
			color: "#333333",
		},
		link: {
			color: "#007AFF",
		},
	}}
/>;
```

### Combining Style Props

You can combine `style`, `textStyle`, and `customStyles` for maximum flexibility:

```tsx
<TermsOfService
	style={{
		padding: 20,
		backgroundColor: "#ffffff",
	}}
	textStyle={{
		fontSize: 16,
		fontFamily: "System",
	}}
	customStyles={{
		h1: {
			fontSize: 28,
			fontWeight: "bold",
		},
		p: {
			lineHeight: 26, // Overrides textStyle lineHeight
		},
	}}
/>
```

### Styleable Elements

The following markdown elements can be styled:

| Element           | `customStyles` Key      | Type        | Description           |
| ----------------- | ----------------------- | ----------- | --------------------- |
| Container         | `container`             | `ViewStyle` | Outer wrapper View    |
| Body              | `body`                  | `TextStyle` | Base text styles      |
| Heading 1         | `h1` or `heading1`      | `TextStyle` | Main headings         |
| Heading 2         | `h2` or `heading2`      | `TextStyle` | Section headings      |
| Heading 3         | `h3` or `heading3`      | `TextStyle` | Subsection headings   |
| Heading 4         | `h4`                    | `TextStyle` | Level 4 headings      |
| Heading 5         | `h5`                    | `TextStyle` | Level 5 headings      |
| Heading 6         | `h6`                    | `TextStyle` | Level 6 headings      |
| Paragraph         | `p` or `paragraph`      | `TextStyle` | Text paragraphs       |
| Unordered list    | `ul` or `bullet_list`   | `ViewStyle` | Bullet lists          |
| Ordered list      | `ol` or `ordered_list`  | `ViewStyle` | Numbered lists        |
| List item         | `li` or `listItem`      | `TextStyle` | Individual list items |
| Link              | `a` or `link`           | `TextStyle` | Hyperlinks            |
| Strong/Bold       | `strong`                | `TextStyle` | Bold text             |
| Emphasis/Italic   | `em`                    | `TextStyle` | Italic text           |
| Inline code       | `code` or `code_inline` | `TextStyle` | Inline code snippets  |
| Code block        | `pre` or `code_block`   | `ViewStyle` | Code blocks           |
| Blockquote        | `blockquote`            | `ViewStyle` | Quoted text           |
| Horizontal rule   | `hr`                    | `ViewStyle` | Dividers              |
| Table             | `table`                 | `ViewStyle` | Tables                |
| Table head        | `thead`                 | `ViewStyle` | Table header          |
| Table body        | `tbody`                 | `ViewStyle` | Table body            |
| Table row         | `tr`                    | `ViewStyle` | Table rows            |
| Table header cell | `th`                    | `TextStyle` | Header cells          |
| Table data cell   | `td`                    | `TextStyle` | Data cells            |
| Text              | `text`                  | `TextStyle` | General text          |

### Common Styling Examples

#### Dark Mode

```tsx
<TermsOfService
	theme="dark"
	customStyles={{
		container: {
			backgroundColor: "#1f2937",
		},
		body: {
			color: "#f9fafb",
		},
		h1: { color: "#ffffff" },
		p: { color: "#d1d5db" },
		a: { color: "#60a5fa" },
	}}
/>
```

#### Compact Design

```tsx
<TermsOfService
	customStyles={{
		container: {
			padding: 16,
		},
		h1: {
			fontSize: 22,
			marginTop: 16,
			marginBottom: 12,
		},
		h2: {
			fontSize: 18,
			marginTop: 14,
			marginBottom: 10,
		},
		p: {
			fontSize: 14,
			lineHeight: 20,
			marginBottom: 12,
		},
		li: {
			fontSize: 14,
			marginBottom: 6,
		},
	}}
/>
```

#### Custom Font Family

```tsx
<TermsOfService
	textStyle={{
		fontFamily: "Georgia",
	}}
	customStyles={{
		h1: {
			fontFamily: "Georgia",
			fontWeight: "bold",
		},
		code: {
			fontFamily: "Courier",
		},
	}}
/>
```

#### Platform-Specific Styles

```tsx
import { Platform } from "react-native";

<TermsOfService
	customStyles={{
		h1: {
			fontSize: Platform.OS === "ios" ? 28 : 26,
			fontWeight: Platform.OS === "ios" ? "600" : "bold",
		},
		p: {
			fontSize: Platform.OS === "ios" ? 16 : 15,
			lineHeight: Platform.OS === "ios" ? 24 : 22,
		},
	}}
/>;
```

### Style Precedence

Styles are applied in the following order (later styles override earlier ones):

1. Base styles (from `react-native-markdown-display`)
2. `textStyle` prop (for text elements)
3. `customStyles` prop (element-specific styles)

### TypeScript Support

All style props are fully typed:

```tsx
import type { DocumentComponentProps } from "appclerk-react-native";
import type { ViewStyle, TextStyle } from "react-native";

const customStyles: DocumentComponentProps["customStyles"] = {
	h1: {
		fontSize: 28,
		fontWeight: "bold",
	},
	// TypeScript will autocomplete and validate all available keys
};
```

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
