<!-- omit in toc -->
# Contributing to OpenGRC

First off, thanks for taking the time to contribute! ❤️

All types of contributions are encouraged and valued. See the [Table of Contents](#table-of-contents) for different ways to help and details about how this project handles them. Please make sure to read the relevant section before making your contribution. It will make it a lot easier for us maintainers and smooth out the experience for all involved. The community looks forward to your contributions. 🎉

> And if you like the project, but just don't have time to contribute, that's fine. There are other easy ways to support the project and show your appreciation, which we would also be very happy about:
> - Star the project
> - Tweet about it
> - Refer this project in your project's readme
> - Mention the project at local meetups and tell your friends/colleagues

<!-- omit in toc -->
## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [I Have a Question](#i-have-a-question)
  - [I Want To Contribute](#i-want-to-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Your First Code Contribution](#your-first-code-contribution)
  - [AI-Assisted Development](#ai-assisted-development)
  - [Improving The Documentation](#improving-the-documentation)
- [Styleguides](#styleguides)
  - [Code Formatting](#code-formatting)
  - [PHP Style Guide](#php-style-guide)
  - [Laravel Style Guide](#laravel-style-guide)
  - [Filament Style Guide](#filament-style-guide)
  - [Enums](#enums)
  - [Testing](#testing)
  - [Commit Messages](#commit-messages)
- [Join The Project Team](#join-the-project-team)


## Code of Conduct

This project and everyone participating in it is governed by the
[OpenGRC Code of Conduct](https://github.com/LeeMangold/OpenGRC/blob//CODE_OF_CONDUCT.md).
By participating, you are expected to uphold this code. Please report unacceptable behavior
to <lee@opengrc.com>.


## I Have a Question

> If you want to ask a question, we assume that you have read the available [Documentation](https://docs.opengrc.com).

Before you ask a question, it is best to search for existing [Issues](https://github.com/LeeMangold/OpenGRC/issues) that might help you. In case you have found a suitable issue and still need clarification, you can write your question in this issue. It is also advisable to search the internet for answers first.

If you then still feel the need to ask a question and need clarification, we recommend the following:

- Open an [Issue](https://github.com/LeeMangold/OpenGRC/issues/new).
- Provide as much context as you can about what you're running into.
- Provide project and platform versions (nodejs, npm, etc), depending on what seems relevant.

We will then take care of the issue as soon as possible.

<!--
You might want to create a separate issue tag for questions and include it in this description. People should then tag their issues accordingly.

Depending on how large the project is, you may want to outsource the questioning, e.g. to Stack Overflow or Gitter. You may add additional contact and information possibilities:
- IRC
- Slack
- Gitter
- Stack Overflow tag
- Blog
- FAQ
- Roadmap
- E-Mail List
- Forum
-->

## I Want To Contribute

> ### Legal Notice <!-- omit in toc -->
> When contributing to this project, you must agree that you have authored 100% of the content, that you have the necessary rights to the content and that the content you contribute may be provided under the project licence.

### Reporting Bugs

<!-- omit in toc -->
#### Before Submitting a Bug Report

A good bug report shouldn't leave others needing to chase you up for more information. Therefore, we ask you to investigate carefully, collect information and describe the issue in detail in your report. Please complete the following steps in advance to help us fix any potential bug as fast as possible.

- Make sure that you are using the latest version.
- Determine if your bug is really a bug and not an error on your side e.g. using incompatible environment components/versions (Make sure that you have read the [documentation](https://docs.opengrc.com). If you are looking for support, you might want to check [this section](#i-have-a-question)).
- To see if other users have experienced (and potentially already solved) the same issue you are having, check if there is not already a bug report existing for your bug or error in the [bug tracker](https://github.com/LeeMangold/OpenGRC/issues?q=label%3Abug).
- Also make sure to search the internet (including Stack Overflow) to see if users outside of the GitHub community have discussed the issue.
- Collect information about the bug:
  - Stack trace (Traceback)
  - OS, Platform and Version (Windows, Linux, macOS, x86, ARM)
  - Version of the interpreter, compiler, SDK, runtime environment, package manager, depending on what seems relevant.
  - Possibly your input and the output
  - Can you reliably reproduce the issue? And can you also reproduce it with older versions?

<!-- omit in toc -->
#### How Do I Submit a Good Bug Report?

> You must never report security related issues, vulnerabilities or bugs including sensitive information to the issue tracker, or elsewhere in public. Instead sensitive bugs must be sent by email to <security@opengrc.com>.
<!-- You may add a PGP key to allow the messages to be sent encrypted as well. -->

We use GitHub issues to track bugs and errors. If you run into an issue with the project:

- Open an [Issue](https://github.com/LeeMangold/OpenGRC/issues/new). (Since we can't be sure at this point whether it is a bug or not, we ask you not to talk about a bug yet and not to label the issue.)
- Explain the behavior you would expect and the actual behavior.
- Please provide as much context as possible and describe the *reproduction steps* that someone else can follow to recreate the issue on their own. This usually includes your code. For good bug reports you should isolate the problem and create a reduced test case.
- Provide the information you collected in the previous section.

Once it's filed:

- The project team will label the issue accordingly.
- A team member will try to reproduce the issue with your provided steps. If there are no reproduction steps or no obvious way to reproduce the issue, the team will ask you for those steps and mark the issue as `needs-repro`. Bugs with the `needs-repro` tag will not be addressed until they are reproduced.
- If the team is able to reproduce the issue, it will be marked `needs-fix`, as well as possibly other tags (such as `critical`), and the issue will be left to be [implemented by someone](#your-first-code-contribution).

<!-- You might want to create an issue template for bugs and errors that can be used as a guide and that defines the structure of the information to be included. If you do so, reference it here in the description. -->


### Suggesting Enhancements

This section guides you through submitting an enhancement suggestion for OpenGRC, **including completely new features and minor improvements to existing functionality**. Following these guidelines will help maintainers and the community to understand your suggestion and find related suggestions.

<!-- omit in toc -->
#### Before Submitting an Enhancement

- Make sure that you are using the latest version.
- Read the [documentation](https://docs.opengrc.com) carefully and find out if the functionality is already covered, maybe by an individual configuration.
- Perform a [search](https://github.com/LeeMangold/OpenGRC/issues) to see if the enhancement has already been suggested. If it has, add a comment to the existing issue instead of opening a new one.
- Find out whether your idea fits with the scope and aims of the project. It's up to you to make a strong case to convince the project's developers of the merits of this feature. Keep in mind that we want features that will be useful to the majority of our users and not just a small subset. If you're just targeting a minority of users, consider writing an add-on/plugin library.

<!-- omit in toc -->
#### How Do I Submit a Good Enhancement Suggestion?

Enhancement suggestions are tracked as [GitHub issues](https://github.com/LeeMangold/OpenGRC/issues).

- Use a **clear and descriptive title** for the issue to identify the suggestion.
- Provide a **step-by-step description of the suggested enhancement** in as many details as possible.
- **Describe the current behavior** and **explain which behavior you expected to see instead** and why. At this point you can also tell which alternatives do not work for you.
- You may want to **include screenshots or screen recordings** which help you demonstrate the steps or point out the part which the suggestion is related to. You can use [LICEcap](https://www.cockos.com/licecap/) to record GIFs on macOS and Windows, and the built-in [screen recorder in GNOME](https://help.gnome.org/users/gnome-help/stable/screen-shot-record.html.en) or [SimpleScreenRecorder](https://github.com/MaartenBaert/ssr) on Linux. <!-- this should only be included if the project has a GUI -->
- **Explain why this enhancement would be useful** to most OpenGRC users. You may also want to point out the other projects that solved it better and which could serve as inspiration.

<!-- You might want to create an issue template for enhancement suggestions that can be used as a guide and that defines the structure of the information to be included. If you do so, reference it here in the description. -->

### Your First Code Contribution
<!-- TODO
include Setup of env, IDE and typical getting started instructions?

-->

### AI-Assisted Development

We welcome and expect contributors to use AI and AI-assisted tools in their workflow. These tools can be a tremendous force for good, accelerating development and helping produce higher-quality contributions.

We recommend using [Laravel Boost](https://laravel.com/ai/boost) for AI-assisted Laravel development. It provides version-specific documentation, database schema access, and other tools that help AI assistants write correct, idiomatic code for this project.

However, AI-generated content requires human oversight. Before committing any AI-assisted work:

- **Proofread thoroughly** - AI can produce plausible-sounding but incorrect content
- **Validate all code** - Test that it actually works as intended
- **Verify facts and references** - AI can hallucinate documentation links, API details, and technical specifications
- **Review for security** - Ensure no vulnerabilities or sensitive data have been introduced

You are responsible for the code you submit, regardless of how it was generated.

### Improving The Documentation
<!-- TODO
Updating, improving and correcting the documentation

-->

## Styleguides

### Code Formatting

We use [Laravel Pint](https://laravel.com/docs/pint) for code formatting. Before submitting a pull request, run:

```bash
vendor/bin/pint
```

For static analysis, we use PHPStan at level 2:

```bash
vendor/bin/phpstan
```

### PHP Style Guide

#### General Rules
- Always use curly braces for control structures, even for single-line statements
- Use explicit return type declarations for all methods and functions
- Use PHP 8 constructor property promotion where applicable
- Prefer descriptive variable and method names (e.g., `isRegisteredForAudit`, not `audit()`)

#### Type Declarations
```php
// Good
protected function isAccessible(User $user, ?string $path = null): bool
{
    // ...
}

// Good - Constructor property promotion
public function __construct(
    public string $name,
    protected AuditService $auditService
) {}
```

#### Comments and Documentation
- Prefer PHPDoc blocks over inline comments
- Add array shape type definitions for complex arrays when appropriate
- Only add inline comments for genuinely complex logic

### Laravel Style Guide

#### General Principles
- Use `php artisan make:*` commands to create new files
- Follow existing directory structure; don't create new base folders without discussion
- Use environment variables only in config files (`config('app.name')`, not `env('APP_NAME')`)

#### Database & Eloquent
- Always use Eloquent relationship methods with return type hints
- Prefer `Model::query()` over `DB::` facade for queries
- Use eager loading to prevent N+1 query problems
- Use Laravel's query builder for complex database operations

```php
// Good - Eager loading
$audits = Audit::with(['items', 'items.control'])->get();

// Avoid - N+1 problem
$audits = Audit::all();
foreach ($audits as $audit) {
    echo $audit->items->count(); // Additional query per audit
}
```

#### Controllers & Validation
- Create Form Request classes for validation (not inline validation)
- Check sibling Form Requests for conventions (array vs string-based rules)

```php
// Good - Form Request
public function store(StoreControlRequest $request): RedirectResponse
{
    Control::create($request->validated());
    return redirect()->route('controls.index');
}
```

#### URL Generation
- Use named routes with the `route()` helper

```php
// Good
return redirect()->route('audits.show', $audit);

// Avoid
return redirect('/audits/' . $audit->id);
```

### Filament Style Guide

OpenGRC uses Filament 3 as the admin panel framework. Follow these conventions:

#### Resources
- Resources live in `app/Filament/Resources/`
- Use `php artisan make:filament-resource` to create new resources
- Resource pages (List, Create, Edit) are auto-generated within the resource's directory

#### Forms
- Use fluent method chaining for form schemas
- Utilize the `relationship()` method on form components when working with related models

```php
Forms\Components\Select::make('program_id')
    ->label('Program')
    ->relationship('program', 'name')
    ->required()
    ->searchable(),
```

#### Tables
- Define sortable and searchable columns where appropriate
- Use bulk actions for common operations

```php
Tables\Columns\TextColumn::make('name')
    ->searchable()
    ->sortable(),
```

#### Actions
- Use Filament Actions for one-time operations (delete, send email, etc.)
- Actions encapsulate UI, modal, and logic in one place

#### Relation Managers
- Use relation managers for managing related data (e.g., `AuditItemRelationManager`)
- Create via `php artisan make:filament-relation-manager`

### Enums

- Enum keys should be TitleCase (e.g., `InProgress`, `NotStarted`)
- Enums live in `app/Enums/`
- All enums should support localization for labels

```php
enum WorkflowStatus: string
{
    case NotStarted = 'not_started';
    case InProgress = 'in_progress';
    case Completed = 'completed';

    public function getLabel(): string
    {
        return match($this) {
            self::NotStarted => __('Not Started'),
            self::InProgress => __('In Progress'),
            self::Completed => __('Completed'),
        };
    }
}
```

### Testing

- Write tests using PHPUnit (not Pest)
- Create tests with `php artisan make:test`
- Use factories when creating models in tests
- Feature tests are preferred over unit tests for most functionality

```bash
# Run all tests
php artisan test

# Run specific test file
php artisan test tests/Feature/AuditTest.php

# Run specific test method
php artisan test --filter=test_user_can_create_audit
```

#### Filament Testing
```php
use function Pest\Livewire\livewire;

// Testing a resource table
livewire(ListControls::class)
    ->assertCanSeeTableRecords($controls)
    ->searchTable('NIST')
    ->assertCanSeeTableRecords($filteredControls);

// Testing resource creation
livewire(CreateControl::class)
    ->fillForm([
        'name' => 'Test Control',
        'code' => 'TC-001',
    ])
    ->call('create')
    ->assertHasNoFormErrors();
```

### Commit Messages

- Use clear, descriptive commit messages
- Start with a verb in present tense (Add, Fix, Update, Remove)
- Reference issue numbers when applicable

```
Add audit export functionality (#123)
Fix N+1 query in controls listing
Update NIST framework import to 2.0
Remove deprecated risk calculation method
```

<!-- omit in toc -->
## Attribution
This guide is based on the [contributing.md](https://contributing.md/generator)!
