Below is a list of future enhancements and features for the Sandcastle tools and the Sandcastle Help File Builder.  No planned release dates have been set for these items.  Each item may be implemented all at once or a little at a time depending on its scope and complexity.  If you'd like to comment on any of these, please do so on the related issue page (see the links below) or, to make additional suggestions, open a new issue.

## Sandcastle Tools
* Investigate the possibility of having *BuildAssembler* build topics in parallel.  That would require that all build components in the stack are thread-safe though.  Possible changes and issues:
  * Add a configuration property to enable parallel builds but default to the current synchronous build behavior.
  * All build components would need an overriden virtual property to indicate if they support parallel execution.  The default if not overridden would be false.  Each build component and syntax generator would need checking to make sure it is thread-safe.  For components that contain nested components, they would need to check each nested component too.
  * Concurrent updates to static members.  Use thread-safe constructs where needed.
  * Use of non-thread-safe objects like the code colorizer.  Wrap them in ThreadLocal<T>?
  * Copying of content files.  Track source and destination files to copy in thread-safe constructs.  Then, when the component is disposed of, copy the content.
  * [Issue #2](https://github.com/EWSoftware/SHFB/issues/2).
* Investigate whether or not a folder name can safely be introduced into the GUID and hashed member name naming methods to reduce the number of files in the root HTML output folder. [Issue #4](https://github.com/EWSoftware/SHFB/issues/4).
* As time permits, add more information to the Sandcastle tools help file that describes the various tools and how they work. [Issue #1](https://github.com/EWSoftware/SHFB/issues/1).
