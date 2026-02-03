# Contributing to Shopify-Zoho Refund Automation

Thank you for your interest in contributing to this project! 🎉

This document provides guidelines for contributing to the Shopify-Zoho Inventory Refund Automation project.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Contribution Workflow](#contribution-workflow)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Community](#community)

---

## 🤝 Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for everyone, regardless of:
- Experience level
- Gender identity and expression
- Sexual orientation
- Disability
- Personal appearance
- Body size
- Race
- Ethnicity
- Age
- Religion
- Nationality

### Expected Behavior

- Be respectful and considerate
- Use welcoming and inclusive language
- Accept constructive criticism gracefully
- Focus on what's best for the community
- Show empathy towards others

### Unacceptable Behavior

- Harassment or discrimination
- Trolling or insulting comments
- Publishing private information without permission
- Any conduct that would be inappropriate in a professional setting

---

## 🎯 How Can I Contribute?

### 1. 🐛 Report Bugs

Found a bug? Help us improve!

**Before Submitting:**
- Check existing [issues](https://github.com/Sohail-crdriod/shopify-zoho-refund-automation/issues)
- Verify it's not a known limitation
- Test with the latest version

**Bug Report Template:**

```markdown
### Bug Description
[Clear description of the bug]

### Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

### Expected Behavior
[What should happen]

### Actual Behavior
[What actually happens]

### Screenshots
[If applicable]

### Environment
- Zoho Flow Version: [e.g., Latest]
- Shopify Store: [e.g., Standard Plan]
- Zoho Inventory: [e.g., Free Plan]
- Date Occurred: [e.g., 2026-02-01]

### Error Logs
```
[Paste error logs here]
```

### Additional Context
[Any other relevant information]
```

### 2. 💡 Suggest Features

Have an idea? We'd love to hear it!

**Feature Request Template:**

```markdown
### Feature Title
[Clear, concise title]

### Problem Statement
[What problem does this solve?]

### Proposed Solution
[How should it work?]

### Alternatives Considered
[Other approaches you thought about]

### Benefits
- Benefit 1
- Benefit 2

### Implementation Complexity
[ ] Low  [ ] Medium  [ ] High

### Priority
[ ] Nice to Have  [ ] Important  [ ] Critical
```

### 3. 📝 Improve Documentation

Documentation improvements are always welcome!

**Documentation Contributions:**
- Fix typos or grammatical errors
- Add missing explanations
- Create diagrams or flowcharts
- Write tutorials or guides
- Translate to other languages
- Add code examples

### 4. 💻 Submit Code

Ready to code? Awesome!

**What You Can Work On:**
- Bug fixes
- New features
- Performance improvements
- Code refactoring
- Test coverage
- Security enhancements

---

## 🛠️ Development Setup

### Prerequisites

1. **Zoho Flow Account**
   - Sign up at https://flow.zoho.com
   - Free plan is sufficient for development

2. **Test Shopify Store**
   - Create a development store
   - Install necessary apps
   - Generate API credentials

3. **Zoho Inventory Test Organization**
   - Set up test organization
   - Add sample products
   - Create test sales orders

### Environment Setup

```bash
# 1. Fork the repository
# Visit: https://github.com/Sohail-crdriod/shopify-zoho-refund-automation
# Click "Fork" button

# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/shopify-zoho-refund-automation.git
cd shopify-zoho-refund-automation

# 3. Add upstream remote
git remote add upstream https://github.com/Sohail-crdriod/shopify-zoho-refund-automation.git

# 4. Create development branch
git checkout -b dev/your-feature-name
```

### Testing Environment

**Test Data Setup:**

1. Create test products in Zoho Inventory
2. Add test customers
3. Create sample sales orders
4. Configure test Shopify store
5. Set up webhook endpoints

**Configuration:**

```deluge
// Test configuration variables
organization_id = "test_org_id";
test_mode = true;
debug_logging = true;
```

---

## 🔄 Contribution Workflow

### Step-by-Step Process

#### 1. Create an Issue

```markdown
Before starting work, create an issue or comment on an existing one to:
- Discuss your approach
- Get feedback from maintainers
- Avoid duplicate work
```

#### 2. Fork & Branch

```bash
# Create a feature branch
git checkout -b feature/add-credit-note-automation

# Or for bug fixes
git checkout -b bugfix/fix-quantity-validation
```

**Branch Naming Convention:**
- `feature/` - New features
- `bugfix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `test/` - Adding tests
- `hotfix/` - Urgent production fixes

#### 3. Make Changes

**Commit Message Format:**

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code formatting (no functional changes)
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples:**

```bash
# Good commit messages
git commit -m "feat(api): Add credit note generation"
git commit -m "fix(validation): Handle null quantities correctly"
git commit -m "docs(readme): Update installation instructions"

# Bad commit messages
git commit -m "fixed stuff"
git commit -m "update"
git commit -m "changes"
```

#### 4. Test Your Changes

```deluge
// Run tests before committing
test_prepareSalesReturnAPI();
test_removeHashFromID();

// Check logs
info "Test completed successfully";
```

#### 5. Push to Your Fork

```bash
# Push your branch
git push origin feature/add-credit-note-automation
```

#### 6. Create Pull Request

**Pull Request Template:**

```markdown
### Description
[Clear description of what this PR does]

### Related Issue
Fixes #123

### Changes Made
- Change 1
- Change 2
- Change 3

### Testing Done
- [ ] Tested locally
- [ ] All existing tests pass
- [ ] Added new tests (if applicable)
- [ ] Tested in staging environment
- [ ] Tested with real data

### Screenshots
[If applicable]

### Checklist
- [ ] Code follows style guidelines
- [ ] Documentation updated
- [ ] No breaking changes
- [ ] Commit messages are clear
- [ ] PR title is descriptive

### Additional Notes
[Any other context]
```

#### 7. Code Review

- Maintainers will review your PR
- Address feedback promptly
- Make requested changes
- Push updates to the same branch

#### 8. Merge

Once approved:
- PR will be merged by maintainers
- Your branch will be deleted
- You'll be credited in release notes!

---

## 📏 Coding Standards

### Deluge Code Style

#### Naming Conventions

```deluge
// Variables: camelCase
myVariable = "value";
itemCount = 10;

// Functions: camelCase
string removeHashFromID(string input_string)

// Constants: UPPER_SNAKE_CASE
MAX_RETRY_COUNT = 3;
API_TIMEOUT = 30;

// Maps/Lists: descriptive names
customerMap = Map();
lineItems = List();
```

#### Code Structure

```deluge
/**
 * Function documentation
 * @param input - Description
 * @return - Description
 */
map myFunction(string input)
{
    // 1. Initialize variables
    result = Map();
    
    // 2. Validation
    if(input == null || input.length() == 0)
    {
        return errorResponse();
    }
    
    // 3. Main logic
    // ... processing ...
    
    // 4. Return result
    return result;
}
```

#### Comments

```deluge
// Single-line comments for brief explanations
salesReturnMap.put("date", today);

/**
 * Multi-line comments for:
 * - Function documentation
 * - Complex logic explanation
 * - Important notes
 */
 
// TODO: Add retry logic
// FIXME: Handle edge case for partial refunds
// NOTE: This assumes all items are invoiced
```

#### Error Handling

```deluge
try
{
    response = zoho.inventory.createRecord(...);
    
    if(response.get("code") == 0)
    {
        // Success path
        return successResponse(response);
    }
    else
    {
        // API error
        return errorResponse(response.get("message"));
    }
}
catch (e)
{
    // Exception handling
    info "Exception: " + e.toString();
    return exceptionResponse(e);
}
```

### Code Quality Checklist

- [ ] Code is readable and self-explanatory
- [ ] Variable names are descriptive
- [ ] Functions are single-purpose
- [ ] No hardcoded values (use variables/constants)
- [ ] Error handling is comprehensive
- [ ] Logging is informative
- [ ] Edge cases are handled
- [ ] Code is DRY (Don't Repeat Yourself)
- [ ] Performance is optimized
- [ ] Security best practices followed

---

## 🧪 Testing Guidelines

### Test Scenarios

#### 1. Unit Tests

Test individual functions:

```deluge
// Test: removeHashFromID
void test_removeHashFromID()
{
    // Test case 1: With hash
    assert(removeHashFromID("#1167") == "1167");
    
    // Test case 2: Without hash
    assert(removeHashFromID("1167") == "1167");
    
    // Test case 3: Empty string
    assert(removeHashFromID("") == "");
    
    info "All tests passed!";
}
```

#### 2. Integration Tests

Test API interactions:

```deluge
// Test: Shopify to Zoho flow
void test_shopifyToZohoIntegration()
{
    // 1. Create test refund in Shopify
    // 2. Trigger automation
    // 3. Verify sales return created in Zoho
    // 4. Check email sent
    // 5. Validate data accuracy
}
```

#### 3. Edge Case Tests

Test unusual scenarios:

```deluge
// Test: All items already returned
// Test: SKU not found
// Test: Partial refund
// Test: Multiple line items
// Test: Zero quantity refund
// Test: API timeout
```

### Testing Checklist

Before submitting PR:

- [ ] All existing tests pass
- [ ] New tests added for new features
- [ ] Edge cases covered
- [ ] Error scenarios tested
- [ ] Manual testing done
- [ ] Logs reviewed for errors
- [ ] Performance benchmarked

---

## 📚 Documentation

### What to Document

1. **Code Comments**
   - Inline explanations for complex logic
   - Function documentation (parameters, return values)
   - Important notes and warnings

2. **README Updates**
   - New features description
   - Updated installation steps
   - Changed configuration
   - New examples

3. **API Documentation**
   - Endpoint details
   - Request/response formats
   - Error codes
   - Rate limits

4. **User Guides**
   - Step-by-step tutorials
   - Screenshots
   - Video walkthroughs
   - FAQs

### Documentation Style

**Clear & Concise:**
```markdown
✅ Good: "This function removes the hash symbol from order IDs."
❌ Bad: "This is a function that does stuff with strings."
```

**Use Examples:**
```markdown
Example:
Input:  "#1167"
Output: "1167"
```

**Visual Aids:**
```markdown
Include:
- Screenshots
- Diagrams
- Flowcharts
- Code snippets
```

---

## 💬 Community

### Get Help

- **GitHub Discussions**: Ask questions, share ideas
- **Issues**: Report bugs, request features
- **Email**: sohail@mtabtechnology.com

### Stay Updated

- **Star** ⭐ the repository
- **Watch** 👀 for updates
- **Follow** the author on GitHub

### Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Credited in documentation
- Featured in README (significant contributions)

---

## 🎖️ Contributor Levels

### 🌱 New Contributor
- First-time contributor
- Fixed typos or minor issues
- Added documentation

### 🌿 Regular Contributor
- 3+ merged PRs
- Helped with code reviews
- Answered community questions

### 🌳 Core Contributor
- 10+ merged PRs
- Major feature development
- Mentors other contributors

### 🌟 Maintainer
- Project leadership
- Makes final decisions
- Manages releases

---

## 🙏 Thank You!

Your contributions make this project better for everyone!

**Questions?**
Don't hesitate to ask. We're here to help! 😊

---

<div align="center">

Made with ❤️ by the Shopify-Zoho Automation Community

[GitHub](https://github.com/Sohail-crdriod/shopify-zoho-refund-automation) • [Issues](https://github.com/Sohail-crdriod/shopify-zoho-refund-automation/issues) • [Discussions](https://github.com/Sohail-crdriod/shopify-zoho-refund-automation/discussions)

</div>
