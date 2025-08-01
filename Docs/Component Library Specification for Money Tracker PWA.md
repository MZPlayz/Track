# Component Library Specification for Money Tracker PWA

**Author:** Manus AI  
**Date:** January 8, 2025  
**Version:** 1.0  

## 1. Introduction

This document specifies the component library for the Money Tracker Progressive Web Application (PWA). The application will primarily utilize components from ShadCN/UI, built on Radix UI primitives and styled with Tailwind CSS. This specification details the core components, their properties (props), states, and how they will be customized to meet the application's design and functional requirements. The goal is to ensure consistency, reusability, accessibility, and efficient development for the AI Coder.

## 2. Component Philosophy

The component library adheres to the following principles:

*   **Reusability:** Components are designed to be highly reusable across different parts of the application.
*   **Modularity:** Components are self-contained and have clear responsibilities.
*   **Accessibility:** All components will be built with accessibility (WCAG 2.1 AA) in mind, leveraging Radix UI's robust accessibility features.
*   **Customizability:** Leveraging ShadCN/UI's approach, components will be easily customizable via Tailwind CSS classes and variants.
*   **Consistency:** A consistent look, feel, and behavior across the entire application.
*   **Performance:** Components are optimized for rendering performance and efficient updates.

## 3. Core Component Categories

Components are categorized based on their function and complexity:

*   **Base Components:** Fundamental UI elements (e.g., Button, Input, Card) that form the building blocks.
*   **Data Display Components:** Components specifically designed for presenting financial data (e.g., Charts, Progress Indicators, Amount Display).
*   **Navigation Components:** Elements facilitating user navigation (e.g., Tabs, Navigation Bar).
*   **Form Components:** Elements for user input and data submission (e.g., Select, Checkbox, Radio Group).
*   **Feedback Components:** Components providing user feedback (e.g., Toast, Dialog, Alert).

## 4. Base Components (ShadCN/UI Customizations)

This section details the customization and usage of fundamental ShadCN/UI components.

### 4.1. Button

**Description:** A clickable element used to trigger actions.
**ShadCN/UI Base:** `components/ui/button.tsx`
**Customizations:**
*   **Variants:** `default`, `destructive`, `outline`, `secondary`, `ghost`, `link`, `success` (new custom variant for positive actions).
*   **Sizes:** `default`, `sm`, `lg`, `icon`.
*   **Colors:** Defined by Tailwind CSS theme (see Design Document).
*   **Hover States:** Subtle background color change and slight scale transformation.
*   **Focus States:** High-contrast outline.
*   **Disabled State:** Reduced opacity, no pointer events.

**Props:**
*   `variant`: (string) - `default | destructive | outline | secondary | ghost | link | success`
*   `size`: (string) - `default | sm | lg | icon`
*   `asChild`: (boolean) - Renders the button as a child of another component.
*   `onClick`: (function) - Event handler for click.
*   `disabled`: (boolean) - If true, the button is disabled.
*   `children`: (ReactNode) - Content of the button.

**Example Usage:**
```tsx
<Button onClick={handleSave} variant="success" size="lg">
  <SaveIcon className="mr-2 h-4 w-4" /> Save Changes
</Button>
```

### 4.2. Input

**Description:** A text input field for user data entry.
**ShadCN/UI Base:** `components/ui/input.tsx`
**Customizations:**
*   **Border Radius:** `6px` (rounded-md).
*   **Focus Ring:** Accent blue (`ring-accent-blue-500`).
*   **Error State:** Red border (`border-alert-red-500`).
*   **Number Input Formatting:** Automatic currency symbol and decimal handling (implemented via custom component wrapping).

**Props:**
*   `type`: (string) - `text | email | password | number | date`
*   `placeholder`: (string) - Placeholder text.
*   `value`: (string) - Current input value.
*   `onChange`: (function) - Event handler for value change.
*   `disabled`: (boolean) - If true, the input is disabled.
*   `readOnly`: (boolean) - If true, the input is read-only.

**Example Usage:**
```tsx
<Input type="number" placeholder="Enter amount" value={amount} onChange={handleAmountChange} />
```

### 4.3. Card

**Description:** A flexible container for grouping related UI elements and content.
**ShadCN/UI Base:** `components/ui/card.tsx`
**Customizations:**
*   **Shadows:** Subtle `shadow-sm` for default, `shadow-md` on hover for interactive cards.
*   **Border Radius:** `8px` (rounded-lg).
*   **Background:** `bg-slate-100` for secondary containers, `bg-white` for primary content cards.
*   **Header/Footer:** Custom slots for consistent layout of card headers (title, icon, actions) and footers.

**Props:**
*   `children`: (ReactNode) - Content of the card.
*   `className`: (string) - Additional CSS classes.

**Example Usage:**
```tsx
<Card>
  <CardHeader>
    <CardTitle>Monthly Spending</CardTitle>
    <CardDescription>Overview of your expenses this month.</CardDescription>
  </CardHeader>
  <CardContent>
    {/* Chart component here */}
  </CardContent>
</Card>
```

## 5. Data Display Components

### 5.1. AmountDisplay

**Description:** Displays financial amounts with consistent formatting and color coding.
**Custom Component:** Wraps a `<span>` or `<div>` with conditional styling.
**Props:**
*   `amount`: (number) - The financial value to display.
*   `currency`: (string) - Currency symbol (e.g., `$` `€`).
*   `type`: (string) - `income | expense | balance` (determines color).
*   `size`: (string) - `sm | md | lg` (determines font size).
*   `showSign`: (boolean) - If true, always shows `+` or `-` sign.

**Styling Logic:**
*   If `type` is `income` and `amount > 0`, use `text-success-green-500`.
*   If `type` is `expense` and `amount < 0`, use `text-alert-red-500`.
*   Otherwise, use `text-slate-900`.
*   Font sizes based on `size` prop (e.g., `text-lg`, `text-2xl`, `text-4xl`).

**Example Usage:**
```tsx
<AmountDisplay amount={2500.75} currency="$" type="balance" size="lg" />
<AmountDisplay amount={-50.00} currency="$" type="expense" showSign />
```

### 5.2. ProgressBar

**Description:** Visualizes progress towards a goal or budget limit.
**ShadCN/UI Base:** `components/ui/progress.tsx`
**Customizations:**
*   **Color Transition:** Gradient from `accent-blue-500` to `success-green-500` as progress increases.
*   **Labeling:** Displays percentage and optional text label.
*   **Variants:** `linear`, `circular`.

**Props:**
*   `value`: (number) - Current progress value (0-100).
*   `max`: (number) - Maximum value (default 100).
*   `label`: (string) - Optional text label to display.
*   `variant`: (string) - `linear | circular`.
*   `status`: (string) - `onTrack | warning | overBudget` (determines color for budget progress).

**Styling Logic:**
*   For `linear` variant, use `w-full` and `h-2`.
*   For `circular` variant, use SVG for circular path.
*   If `status` is `warning`, use `bg-warning-orange-500`.
*   If `status` is `overBudget`, use `bg-alert-red-500`.

**Example Usage:**
```tsx
<ProgressBar value={75} label="75% complete" variant="linear" />
<ProgressBar value={85} label="Budget Progress" variant="circular" status="warning" />
```

### 5.3. Chart (Wrapper Component)

**Description:** A wrapper component for various chart types (Line, Bar, Pie) using Chart.js or Recharts.
**Custom Component:** Encapsulates chart library logic and provides consistent styling.
**Props:**
*   `type`: (string) - `line | bar | pie`.
*   `data`: (object) - Chart data in a standardized format.
*   `options`: (object) - Chart options (e.g., tooltips, legends).
*   `title`: (string) - Title for the chart.
*   `description`: (string) - Description for accessibility.

**Styling Logic:**
*   Consistent font sizes and colors for labels and legends.
*   Responsive sizing for charts.
*   Accessibility features (ARIA attributes, keyboard navigation).

**Example Usage:**
```tsx
<Chart type="line" data={incomeExpenseData} options={lineChartOptions} title="Income vs. Expense Trend" />
```

## 6. Navigation Components

### 6.1. Tabs

**Description:** A set of layered sections of content, known as tab panels, that are displayed one at a time.
**ShadCN/UI Base:** `components/ui/tabs.tsx`
**Customizations:**
*   **Styling:** Underline indicator for active tab, consistent padding.
*   **Accessibility:** Full keyboard navigation.

**Props:**
*   `defaultValue`: (string) - The value of the tab that should be active by default.
*   `children`: (ReactNode) - `TabsList` and `TabsContent` components.

**Example Usage:**
```tsx
<Tabs defaultValue="overview">
  <TabsList>
    <TabsTrigger value="overview">Overview</TabsTrigger>
    <TabsTrigger value="transactions">Transactions</TabsTrigger>
  </TabsList>
  <TabsContent value="overview">{/* Overview content */}</TabsContent>
  <TabsContent value="transactions">{/* Transactions content */}</TabsContent>
</Tabs>
```

### 6.2. NavigationMenu (for Desktop) / Sheet (for Mobile)

**Description:** Provides primary application navigation.
**ShadCN/UI Base:** `components/ui/navigation-menu.tsx` (Desktop), `components/ui/sheet.tsx` (Mobile)
**Customizations:**
*   **Desktop:** Horizontal menu with dropdowns for sub-sections.
*   **Mobile:** Drawer/sidebar menu accessible via a hamburger icon.
*   **Active State:** Highlight current page link.

**Props (NavigationMenu):**
*   `children`: (ReactNode) - `NavigationMenuList`, `NavigationMenuItem`, `NavigationMenuLink`.

**Props (Sheet):**
*   `open`: (boolean) - Controls visibility.
*   `onOpenChange`: (function) - Callback for open state change.
*   `children`: (ReactNode) - Content of the sheet.

**Example Usage (Conceptual):**
```tsx
// Desktop
<NavigationMenu>
  <NavigationMenuList>
    <NavigationMenuItem><NavigationMenuLink href="/dashboard">Dashboard</NavigationMenuLink></NavigationMenuItem>
  </NavigationMenuList>
</NavigationMenu>

// Mobile
<Sheet>
  <SheetTrigger asChild><Button variant="ghost" size="icon"><MenuIcon /></Button></SheetTrigger>
  <SheetContent side="left">
    {/* Mobile navigation links */}
  </SheetContent>
</Sheet>
```

## 7. Form Components

### 7.1. Select

**Description:** A dropdown menu for selecting a single option from a list.
**ShadCN/UI Base:** `components/ui/select.tsx`
**Customizations:**
*   **Styling:** Consistent with input fields.
*   **Accessibility:** Keyboard navigation, screen reader support.

**Props:**
*   `value`: (string) - Current selected value.
*   `onValueChange`: (function) - Callback for value change.
*   `children`: (ReactNode) - `SelectTrigger`, `SelectContent`, `SelectItem`.

**Example Usage:**
```tsx
<Select onValueChange={handleCategoryChange} defaultValue="Groceries">
  <SelectTrigger className="w-[180px]">
    <SelectValue placeholder="Select a category" />
  </SelectTrigger>
  <SelectContent>
    <SelectItem value="Groceries">Groceries</SelectItem>
    <SelectItem value="Rent">Rent</SelectItem>
  </SelectContent>
</Select>
```

### 7.2. Checkbox

**Description:** A checkbox for boolean input.
**ShadCN/UI Base:** `components/ui/checkbox.tsx`
**Customizations:**
*   **Styling:** Accent blue checkmark.

**Props:**
*   `checked`: (boolean) - Whether the checkbox is checked.
*   `onCheckedChange`: (function) - Callback for checked state change.
*   `id`: (string) - Unique ID for accessibility.

**Example Usage:**
```tsx
<div className="flex items-center space-x-2">
  <Checkbox id="terms" onCheckedChange={handleTermsChange} />
  <label htmlFor="terms">Accept terms and conditions</label>
</div>
```

## 8. Feedback Components

### 8.1. Toast

**Description:** A transient message that appears temporarily to provide feedback to the user.
**ShadCN/UI Base:** `components/ui/toast.tsx` (and `use-toast.ts` hook)
**Customizations:**
*   **Variants:** `success`, `error`, `info`.
*   **Position:** Top right.

**Props (via `toast()` function):**
*   `title`: (string) - Main message.
*   `description`: (string) - Optional detailed message.
*   `variant`: (string) - `default | destructive | success | info`.
*   `duration`: (number) - How long the toast should be visible (ms).

**Example Usage:**
```tsx
import { useToast } from "@/components/ui/use-toast";

const { toast } = useToast();

toast({
  title: "Transaction Added!",
  description: "Your expense has been successfully recorded.",
  variant: "success",
});
```

### 8.2. Dialog

**Description:** A modal dialog for user interaction or information display.
**ShadCN/UI Base:** `components/ui/dialog.tsx`
**Customizations:**
*   **Overlay:** Dimmed background.
*   **Styling:** Consistent with card components.

**Props:**
*   `open`: (boolean) - Controls visibility.
*   `onOpenChange`: (function) - Callback for open state change.
*   `children`: (ReactNode) - `DialogTrigger`, `DialogContent`, `DialogHeader`, `DialogFooter`.

**Example Usage:**
```tsx
<Dialog>
  <DialogTrigger asChild><Button>Add New Transaction</Button></DialogTrigger>
  <DialogContent>
    <DialogHeader>
      <DialogTitle>Add Transaction</DialogTitle>
      <DialogDescription>Enter details for your new transaction.</DialogDescription>
    </DialogHeader>
    {/* Transaction form here */}
    <DialogFooter>
      <Button type="submit">Save</Button>
    </DialogFooter>
  </DialogContent>
</Dialog>
```

## 9. Component Development Guidelines for AI Coder

*   **Prioritize ShadCN/UI:** Always check if a suitable ShadCN/UI component exists before creating a custom one. If it exists, use it and customize it.
*   **Follow ShadCN/UI Structure:** When adding new components, follow the `components/ui` directory structure and `cn` utility for class merging.
*   **Accessibility First:** Ensure all interactive components have proper `aria-*` attributes, keyboard navigation, and focus management.
*   **Type Safety:** Use TypeScript for all component props and state.
*   **Storybook/Documentation:** (Future consideration) Document components with examples and prop tables for easy reference.
*   **Responsive Design:** Implement responsive styling using Tailwind CSS utility classes (e.g., `sm:`, `md:`, `lg:`).
*   **Theming:** Utilize CSS variables and Tailwind CSS configuration for theme-related styling, as defined in the Design Document.
*   **Data Flow:** Components should be primarily presentational, receiving data via props and emitting events via callbacks.

This Component Library Specification provides a detailed guide for building the Money Tracker PWA's frontend, ensuring a consistent, accessible, and efficient development process.

