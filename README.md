# Flutter Custom Widgets Guide

Learn how to create reusable custom widgets in Flutter with practical examples.

## Table of Contents
- [Basic Custom Widget](#basic-custom-widget)
- [Configurable Custom Widget](#configurable-custom-widget)
- [Stateful Custom Widget](#stateful-custom-widget)

---

## Basic Custom Widget

Create simple reusable widgets that wrap common elements.

### Example: CustomCard

```dart
import 'package:flutter/material.dart';

class CustomCard extends StatelessWidget {
  final Widget child;
  
  const CustomCard({
    super.key,
    required this.child,
  });

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 4,
      margin: const EdgeInsets.all(8),
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: child,
      ),
    );
  }
}
```

### Usage:

```dart
CustomCard(
  child: Text('This is inside a custom card'),
)
```

---

## Configurable Custom Widget

A widget with multiple configuration options.

### Example: CustomButton

```dart
class CustomButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;
  final Color color;
  final Color textColor;
  final double borderRadius;
  
  const CustomButton({
    super.key,
    required this.text,
    required this.onPressed,
    this.color = Colors.blue,
    this.textColor = Colors.white,
    this.borderRadius = 8.0,
  });

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      style: ElevatedButton.styleFrom(
        backgroundColor: color,
        foregroundColor: textColor,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(borderRadius),
        ),
        padding: const EdgeInsets.symmetric(horizontal: 24, vertical: 12),
      ),
      onPressed: onPressed,
      child: Text(text),
    );
  }
}
```

### Usage:


```dart
CustomButton(
  text: 'Click Me',
  onPressed: () => print('Button pressed'),
  color: Colors.green,
  borderRadius: 12.0,
)
```

---

## Stateful Custom Widget

A custom widget that maintains its own state.

### Example: ExpandablePanel

```dart
class ExpandablePanel extends StatefulWidget {
  final String header;
  final Widget content;
  
  const ExpandablePanel({
    super.key,
    required this.header,
    required this.content,
  });

  @override
  State<ExpandablePanel> createState() => _ExpandablePanelState();
}

class _ExpandablePanelState extends State<ExpandablePanel> {
  bool _isExpanded = false;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ListTile(
          title: Text(widget.header),
          trailing: Icon(
            _isExpanded ? Icons.expand_less : Icons.expand_more,
          ),
          onTap: () {
            setState(() {
              _isExpanded = !_isExpanded;
            });
          },
        ),
        if (_isExpanded)
          Padding(
            padding: const EdgeInsets.all(16),
            child: widget.content,
          ),
      ],
    );
  }
}
```

### Usage:
```dart
ExpandablePanel(
  header: 'Advanced Settings',
  content: Column(
    children: [
      // Your settings widgets here
    ],
  ),
)
```
