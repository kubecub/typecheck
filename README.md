# Go Typecheck: Cross-Platform Source Code Type Checking for Go

## Introduction

Go Typecheck is a robust tool designed for cross-platform source code type checking across all Go build platforms. This utility leverages Go’s built-in parsing and type-check libraries (`go/parser` and `go/types`) to deliver efficient and reliable code analysis.

## Advantages

- **Speed**: A complete compilation with Go can take approximately 3 minutes. In contrast, Go Typecheck achieves this in mere seconds, significantly enhancing productivity.
- **Resource Efficiency**: Unlike the typical requirement of over 40GB of RAM for standard processes, Typecheck operates effectively with less than 8GB of RAM. This reduction in resource consumption makes it highly suitable for a variety of systems, reducing overheads and facilitating smoother operations.

## Implementation

Go Typecheck employs Go's native parsing and type-checking libraries (`go/parser` and `go/types`). However, it's important to note that these libraries aren't identical to those used by the Go compiler. While occasional mismatches may occur, these libraries generally provide close approximations to the compiler's functionality, offering a reliable basis for type checking.

## Error Handling

Typecheck's approach to error handling is pragmatic, focusing on practicality and build continuity.

**Errors reported by `go/types` but not by `go build`**:
- **Actual Errors** (as per the specification):
  - These should ideally be rectified. If rectification is not feasible, such as in cases of ongoing work or external dependencies in the code, these errors can be overlooked.
    - Example: Unused variables within a closure.
- **False Positives**:
  - These errors should be ignored and, where appropriate, reported upstream for resolution.
    - Example: Type mismatches between staging and generated types.

**Errors reported by `go build` but not by us**:
- CGo-related errors, including both syntax and linker issues, are outside our scope.

## Usage

### Github Actions

To integrate Go Code Typecheck into your GitHub Actions workflow, you can use the action available at the GitHub Marketplace. This action helps in performing type checks on your Go codebase, ensuring type safety and catching potential errors early in the development process.

**Marketplace URL**: [Go Code Typecheck on GitHub Marketplace](https://github.com/marketplace/actions/go-code-typecheck)

**GitHub Repository URL**: [kubecub/typecheck on GitHub](https://github.com/kubecub/typecheck)

To use this action in your workflow, include the following step in your `.github/workflows/<your-workflow>.yml` file:

```yml
- name: Go Code Typecheck
  uses: kubecub/typecheck@v1.0.0
```

The version of the action can be specified by using the tag associated with the desired release of `kubecub/typecheck`. For example, `@v1.0.0` refers to version 0.1.3 of the action.

By incorporating this action into your workflow, you can automatically verify the type correctness of your Go code with every push or pull request, helping maintain code quality and reliability.

### Locally

To run Typecheck locally, simply use the following command:

```bash
make verify
```

### Continuous Integration (CI)

In CI environments, Typecheck can be integrated into the workflow as follows:

```yaml
- name: Typecheck
  run: make verify
```

This streamlined process facilitates efficient error detection and resolution, ensuring a robust and reliable build pipeline.

More to learn about typecheck [share blog](https://nsddd.top/posts/concurrent-type-checking-and-cross-platform-development-in-go/)