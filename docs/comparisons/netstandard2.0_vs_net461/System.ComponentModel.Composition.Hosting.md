# System.ComponentModel.Composition.Hosting

``` diff
+namespace System.ComponentModel.Composition.Hosting {
+    public class AggregateCatalog : ComposablePartCatalog, INotifyComposablePartCatalogChanged {
+        public AggregateCatalog();
+        public AggregateCatalog(IEnumerable<ComposablePartCatalog> catalogs);
+        public AggregateCatalog(params ComposablePartCatalog[] catalogs);
+        public ICollection<ComposablePartCatalog> Catalogs { get; }
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changed;
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changing;
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override IEnumerable<Tuple<ComposablePartDefinition, ExportDefinition>> GetExports(ImportDefinition definition);
+        protected virtual void OnChanged(ComposablePartCatalogChangeEventArgs e);
+        protected virtual void OnChanging(ComposablePartCatalogChangeEventArgs e);
+    }
+    public class AggregateExportProvider : ExportProvider, IDisposable {
+        public AggregateExportProvider(IEnumerable<ExportProvider> providers);
+        public AggregateExportProvider(params ExportProvider[] providers);
+        public ReadOnlyCollection<ExportProvider> Providers { get; }
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        protected override IEnumerable<Export> GetExportsCore(ImportDefinition definition, AtomicComposition atomicComposition);
+    }
+    public class ApplicationCatalog : ComposablePartCatalog, ICompositionElement {
+        public ApplicationCatalog();
+        public ApplicationCatalog(ICompositionElement definitionOrigin);
+        public ApplicationCatalog(ReflectionContext reflectionContext);
+        public ApplicationCatalog(ReflectionContext reflectionContext, ICompositionElement definitionOrigin);
+        string System.ComponentModel.Composition.Primitives.ICompositionElement.DisplayName { get; }
+        ICompositionElement System.ComponentModel.Composition.Primitives.ICompositionElement.Origin { get; }
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override IEnumerable<Tuple<ComposablePartDefinition, ExportDefinition>> GetExports(ImportDefinition definition);
+        public override string ToString();
+    }
+    public class AssemblyCatalog : ComposablePartCatalog, ICompositionElement {
+        public AssemblyCatalog(Assembly assembly);
+        public AssemblyCatalog(Assembly assembly, ICompositionElement definitionOrigin);
+        public AssemblyCatalog(Assembly assembly, ReflectionContext reflectionContext);
+        public AssemblyCatalog(Assembly assembly, ReflectionContext reflectionContext, ICompositionElement definitionOrigin);
+        public AssemblyCatalog(string codeBase);
+        public AssemblyCatalog(string codeBase, ICompositionElement definitionOrigin);
+        public AssemblyCatalog(string codeBase, ReflectionContext reflectionContext);
+        public AssemblyCatalog(string codeBase, ReflectionContext reflectionContext, ICompositionElement definitionOrigin);
+        public Assembly Assembly { get; }
+        string System.ComponentModel.Composition.Primitives.ICompositionElement.DisplayName { get; }
+        ICompositionElement System.ComponentModel.Composition.Primitives.ICompositionElement.Origin { get; }
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override IEnumerable<Tuple<ComposablePartDefinition, ExportDefinition>> GetExports(ImportDefinition definition);
+        public override string ToString();
+    }
+    public class AtomicComposition : IDisposable {
+        public AtomicComposition();
+        public AtomicComposition(AtomicComposition outerAtomicComposition);
+        public void AddCompleteAction(Action completeAction);
+        public void AddRevertAction(Action revertAction);
+        public void Complete();
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        public void SetValue(object key, object value);
+        public bool TryGetValue<T>(object key, bool localAtomicCompositionOnly, out T value);
+        public bool TryGetValue<T>(object key, out T value);
+    }
+    public class CatalogExportProvider : ExportProvider, IDisposable {
+        public CatalogExportProvider(ComposablePartCatalog catalog);
+        public CatalogExportProvider(ComposablePartCatalog catalog, bool isThreadSafe);
+        public CatalogExportProvider(ComposablePartCatalog catalog, CompositionOptions compositionOptions);
+        public ComposablePartCatalog Catalog { get; }
+        public ExportProvider SourceProvider { get; set; }
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        protected override IEnumerable<Export> GetExportsCore(ImportDefinition definition, AtomicComposition atomicComposition);
+    }
+    public static class CatalogExtensions {
+        public static CompositionService CreateCompositionService(this ComposablePartCatalog composablePartCatalog);
+    }
+    public class ComposablePartCatalogChangeEventArgs : EventArgs {
+        public ComposablePartCatalogChangeEventArgs(IEnumerable<ComposablePartDefinition> addedDefinitions, IEnumerable<ComposablePartDefinition> removedDefinitions, AtomicComposition atomicComposition);
+        public IEnumerable<ComposablePartDefinition> AddedDefinitions { get; }
+        public AtomicComposition AtomicComposition { get; private set; }
+        public IEnumerable<ComposablePartDefinition> RemovedDefinitions { get; }
+    }
+    public class ComposablePartExportProvider : ExportProvider, IDisposable {
+        public ComposablePartExportProvider();
+        public ComposablePartExportProvider(bool isThreadSafe);
+        public ComposablePartExportProvider(CompositionOptions compositionOptions);
+        public ExportProvider SourceProvider { get; set; }
+        public void Compose(CompositionBatch batch);
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        protected override IEnumerable<Export> GetExportsCore(ImportDefinition definition, AtomicComposition atomicComposition);
+    }
+    public class CompositionBatch {
+        public CompositionBatch();
+        public CompositionBatch(IEnumerable<ComposablePart> partsToAdd, IEnumerable<ComposablePart> partsToRemove);
+        public ReadOnlyCollection<ComposablePart> PartsToAdd { get; }
+        public ReadOnlyCollection<ComposablePart> PartsToRemove { get; }
+        public ComposablePart AddExport(Export export);
+        public void AddPart(ComposablePart part);
+        public void RemovePart(ComposablePart part);
+    }
+    public static class CompositionConstants {
+        public const string ExportTypeIdentityMetadataName = "ExportTypeIdentity";
+        public const string GenericContractMetadataName = "System.ComponentModel.Composition.GenericContractName";
+        public const string GenericParametersMetadataName = "System.ComponentModel.Composition.GenericParameters";
+        public const string ImportSourceMetadataName = "System.ComponentModel.Composition.ImportSource";
+        public const string IsGenericPartMetadataName = "System.ComponentModel.Composition.IsGenericPart";
+        public const string PartCreationPolicyMetadataName = "System.ComponentModel.Composition.CreationPolicy";
+    }
+    public class CompositionContainer : ExportProvider, ICompositionService, IDisposable {
+        public CompositionContainer();
+        public CompositionContainer(CompositionOptions compositionOptions, params ExportProvider[] providers);
+        public CompositionContainer(params ExportProvider[] providers);
+        public CompositionContainer(ComposablePartCatalog catalog, bool isThreadSafe, params ExportProvider[] providers);
+        public CompositionContainer(ComposablePartCatalog catalog, CompositionOptions compositionOptions, params ExportProvider[] providers);
+        public CompositionContainer(ComposablePartCatalog catalog, params ExportProvider[] providers);
+        public ComposablePartCatalog Catalog { get; }
+        public ReadOnlyCollection<ExportProvider> Providers { get; }
+        public void Compose(CompositionBatch batch);
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        protected override IEnumerable<Export> GetExportsCore(ImportDefinition definition, AtomicComposition atomicComposition);
+        public void ReleaseExport(Export export);
+        public void ReleaseExport<T>(Lazy<T> export);
+        public void ReleaseExports(IEnumerable<Export> exports);
+        public void ReleaseExports<T, TMetadataView>(IEnumerable<Lazy<T, TMetadataView>> exports);
+        public void ReleaseExports<T>(IEnumerable<Lazy<T>> exports);
+        public void SatisfyImportsOnce(ComposablePart part);
+    }
+    public enum CompositionOptions {
+        Default = 0,
+        DisableSilentRejection = 1,
+        ExportCompositionService = 4,
+        IsThreadSafe = 2,
+    }
+    public class CompositionScopeDefinition : ComposablePartCatalog, INotifyComposablePartCatalogChanged {
+        protected CompositionScopeDefinition();
+        public CompositionScopeDefinition(ComposablePartCatalog catalog, IEnumerable<CompositionScopeDefinition> children);
+        public CompositionScopeDefinition(ComposablePartCatalog catalog, IEnumerable<CompositionScopeDefinition> children, IEnumerable<ExportDefinition> publicSurface);
+        public virtual IEnumerable<CompositionScopeDefinition> Children { get; }
+        public virtual IEnumerable<ExportDefinition> PublicSurface { get; }
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changed;
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changing;
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override IEnumerable<Tuple<ComposablePartDefinition, ExportDefinition>> GetExports(ImportDefinition definition);
+        protected virtual void OnChanged(ComposablePartCatalogChangeEventArgs e);
+        protected virtual void OnChanging(ComposablePartCatalogChangeEventArgs e);
+    }
+    public class CompositionService : ICompositionService, IDisposable {
+        public void Dispose();
+        public void SatisfyImportsOnce(ComposablePart part);
+    }
+    public class DirectoryCatalog : ComposablePartCatalog, ICompositionElement, INotifyComposablePartCatalogChanged {
+        public DirectoryCatalog(string path);
+        public DirectoryCatalog(string path, ICompositionElement definitionOrigin);
+        public DirectoryCatalog(string path, ReflectionContext reflectionContext);
+        public DirectoryCatalog(string path, ReflectionContext reflectionContext, ICompositionElement definitionOrigin);
+        public DirectoryCatalog(string path, string searchPattern);
+        public DirectoryCatalog(string path, string searchPattern, ICompositionElement definitionOrigin);
+        public DirectoryCatalog(string path, string searchPattern, ReflectionContext reflectionContext);
+        public DirectoryCatalog(string path, string searchPattern, ReflectionContext reflectionContext, ICompositionElement definitionOrigin);
+        public string FullPath { get; }
+        public ReadOnlyCollection<string> LoadedFiles { get; }
+        public string Path { get; }
+        public string SearchPattern { get; }
+        string System.ComponentModel.Composition.Primitives.ICompositionElement.DisplayName { get; }
+        ICompositionElement System.ComponentModel.Composition.Primitives.ICompositionElement.Origin { get; }
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changed;
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changing;
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override IEnumerable<Tuple<ComposablePartDefinition, ExportDefinition>> GetExports(ImportDefinition definition);
+        protected virtual void OnChanged(ComposablePartCatalogChangeEventArgs e);
+        protected virtual void OnChanging(ComposablePartCatalogChangeEventArgs e);
+        public void Refresh();
+        public override string ToString();
+    }
+    public abstract class ExportProvider {
+        protected ExportProvider();
+        public event EventHandler<ExportsChangeEventArgs> ExportsChanged;
+        public event EventHandler<ExportsChangeEventArgs> ExportsChanging;
+        public Lazy<T, TMetadataView> GetExport<T, TMetadataView>();
+        public Lazy<T, TMetadataView> GetExport<T, TMetadataView>(string contractName);
+        public Lazy<T> GetExport<T>();
+        public Lazy<T> GetExport<T>(string contractName);
+        public T GetExportedValue<T>();
+        public T GetExportedValue<T>(string contractName);
+        public T GetExportedValueOrDefault<T>();
+        public T GetExportedValueOrDefault<T>(string contractName);
+        public IEnumerable<T> GetExportedValues<T>();
+        public IEnumerable<T> GetExportedValues<T>(string contractName);
+        public IEnumerable<Export> GetExports(ImportDefinition definition);
+        public IEnumerable<Export> GetExports(ImportDefinition definition, AtomicComposition atomicComposition);
+        public IEnumerable<Lazy<object, object>> GetExports(Type type, Type metadataViewType, string contractName);
+        public IEnumerable<Lazy<T, TMetadataView>> GetExports<T, TMetadataView>();
+        public IEnumerable<Lazy<T, TMetadataView>> GetExports<T, TMetadataView>(string contractName);
+        public IEnumerable<Lazy<T>> GetExports<T>();
+        public IEnumerable<Lazy<T>> GetExports<T>(string contractName);
+        protected abstract IEnumerable<Export> GetExportsCore(ImportDefinition definition, AtomicComposition atomicComposition);
+        protected virtual void OnExportsChanged(ExportsChangeEventArgs e);
+        protected virtual void OnExportsChanging(ExportsChangeEventArgs e);
+        public bool TryGetExports(ImportDefinition definition, AtomicComposition atomicComposition, out IEnumerable<Export> exports);
+    }
+    public class ExportsChangeEventArgs : EventArgs {
+        public ExportsChangeEventArgs(IEnumerable<ExportDefinition> addedExports, IEnumerable<ExportDefinition> removedExports, AtomicComposition atomicComposition);
+        public IEnumerable<ExportDefinition> AddedExports { get; }
+        public AtomicComposition AtomicComposition { get; private set; }
+        public IEnumerable<string> ChangedContractNames { get; }
+        public IEnumerable<ExportDefinition> RemovedExports { get; }
+    }
+    public class FilteredCatalog : ComposablePartCatalog, INotifyComposablePartCatalogChanged {
+        public FilteredCatalog(ComposablePartCatalog catalog, Func<ComposablePartDefinition, bool> filter);
+        public FilteredCatalog Complement { get; }
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changed;
+        public event EventHandler<ComposablePartCatalogChangeEventArgs> Changing;
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override IEnumerable<Tuple<ComposablePartDefinition, ExportDefinition>> GetExports(ImportDefinition definition);
+        public FilteredCatalog IncludeDependencies();
+        public FilteredCatalog IncludeDependencies(Func<ImportDefinition, bool> importFilter);
+        public FilteredCatalog IncludeDependents();
+        public FilteredCatalog IncludeDependents(Func<ImportDefinition, bool> importFilter);
+        protected virtual void OnChanged(ComposablePartCatalogChangeEventArgs e);
+        protected virtual void OnChanging(ComposablePartCatalogChangeEventArgs e);
+    }
+    public class ImportEngine : ICompositionService, IDisposable {
+        public ImportEngine(ExportProvider sourceProvider);
+        public ImportEngine(ExportProvider sourceProvider, bool isThreadSafe);
+        public ImportEngine(ExportProvider sourceProvider, CompositionOptions compositionOptions);
+        public void Dispose();
+        protected virtual void Dispose(bool disposing);
+        public void PreviewImports(ComposablePart part, AtomicComposition atomicComposition);
+        public void ReleaseImports(ComposablePart part, AtomicComposition atomicComposition);
+        public void SatisfyImports(ComposablePart part);
+        public void SatisfyImportsOnce(ComposablePart part);
+    }
+    public interface INotifyComposablePartCatalogChanged {
+        event EventHandler<ComposablePartCatalogChangeEventArgs> Changed;
+        event EventHandler<ComposablePartCatalogChangeEventArgs> Changing;
+    }
+    public static class ScopingExtensions {
+        public static bool ContainsPartMetadata<T>(this ComposablePartDefinition part, string key, T value);
+        public static bool ContainsPartMetadataWithKey(this ComposablePartDefinition part, string key);
+        public static bool Exports(this ComposablePartDefinition part, string contractName);
+        public static FilteredCatalog Filter(this ComposablePartCatalog catalog, Func<ComposablePartDefinition, bool> filter);
+        public static bool Imports(this ComposablePartDefinition part, string contractName);
+        public static bool Imports(this ComposablePartDefinition part, string contractName, ImportCardinality importCardinality);
+    }
+    public class TypeCatalog : ComposablePartCatalog, ICompositionElement {
+        public TypeCatalog(IEnumerable<Type> types);
+        public TypeCatalog(IEnumerable<Type> types, ICompositionElement definitionOrigin);
+        public TypeCatalog(IEnumerable<Type> types, ReflectionContext reflectionContext);
+        public TypeCatalog(IEnumerable<Type> types, ReflectionContext reflectionContext, ICompositionElement definitionOrigin);
+        public TypeCatalog(params Type[] types);
+        string System.ComponentModel.Composition.Primitives.ICompositionElement.DisplayName { get; }
+        ICompositionElement System.ComponentModel.Composition.Primitives.ICompositionElement.Origin { get; }
+        protected override void Dispose(bool disposing);
+        public override IEnumerator<ComposablePartDefinition> GetEnumerator();
+        public override string ToString();
+    }
+}
```

