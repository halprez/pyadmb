# PyADMB - Python Wrapper for ADMB

A modern Python interface for AD Model Builder (ADMB), bringing automatic differentiation and advanced optimization to fisheries stock assessment and ecological modeling.

## 🎯 Project Vision

PyADMB aims to bridge the gap between ADMB's powerful automatic differentiation capabilities and Python's modern data science ecosystem, making advanced stock assessment modeling accessible to a broader community of researchers and practitioners.

## 🚀 Key Features (Planned)

- **Pythonic Interface**: Clean, intuitive API for defining and running ADMB models.
- **Automatic Multiplatform Installation**: Handle ADMB installation automatically on major platforms (Windows, Linux, MacOS).
- **Seamless Integration**: Works naturally with pandas, numpy, matplotlib, and scikit-learn, and all Python ecosystem.
- **Modern Workflows**: Jupyter notebook support, easy visualization, and reproducible research,
- **Lower Barrier to Entry**: Familiar Python syntax for complex population dynamics models.
- **AI/ML Ready**: Easy integration with machine learning libraries for model diagnostics and hybrid approaches.

## 📋 Implementation Plan

### Phase 0: Explore ADMB intallation and packaging.
- [] Research installation in Windows.
- [] Research installation in Linux.
- [] Research installation in MacOS



### Phase 1: Core Wrapper Infrastructure
**Timeline: 2-3 months**

#### 1.1 Project Setup
- [ ] Repository structure and packaging
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Documentation framework (Sphinx)
- [ ] Testing framework (pytest)

#### 1.2 ADMB Interface Layer
- [ ] ADMB installation detection and validation
- [ ] Template file generation from Python objects
- [ ] Compilation and execution management
- [ ] Output parsing and data extraction
- [ ] Error handling and debugging support

#### 1.3 Core Data Structures
```python
class ADMBModel:
    """Base class for ADMB models"""
    def __init__(self, name: str)
    def add_data(self, data: pd.DataFrame)
    def add_parameters(self, params: dict)
    def compile(self) -> bool
    def run(self) -> ADMBResults
    
class ADMBResults:
    """Container for ADMB output"""
    def to_pandas(self) -> pd.DataFrame
    def plot(self, **kwargs)
    def summary(self) -> dict
```

### Phase 2: Fisheries Stock Assessment Models
**Timeline: 3-4 months**

#### 2.1 Simple Models
- [ ] Surplus Production Models (Schaefer, Pella-Tomlinson)
- [ ] Catch-at-Age Models (basic)
- [ ] Data-limited assessment methods

#### 2.2 Model Templates
```python
# Example: Simple surplus production model
from pyadmb import SurplusProductionModel

model = SurplusProductionModel()
model.set_catch_data(catch_df)
model.set_survey_data(survey_df)
model.set_priors(r=0.5, K=10000, q=0.001)

results = model.fit()
print(results.biomass_trajectory)
results.plot_diagnostics()
```

#### 2.3 Advanced Features
- [ ] Multiple fleet support
- [ ] Environmental covariates
- [ ] State-space models
- [ ] Bayesian estimation options

### Phase 3: Integration & Usability
**Timeline: 2-3 months**

#### 3.1 Data Science Integration
- [ ] Pandas DataFrame native support
- [ ] NumPy array compatibility
- [ ] Matplotlib/Seaborn plotting integration
- [ ] Jupyter notebook optimized displays

#### 3.2 Machine Learning Bridge
```python
# Example: ML-enhanced diagnostics
from pyadmb.diagnostics import MLDiagnostics
from sklearn.ensemble import RandomForestRegressor

diagnostics = MLDiagnostics(model_results)
residual_patterns = diagnostics.analyze_residuals(RandomForestRegressor())
diagnostics.plot_ml_insights()
```

#### 3.3 Workflow Tools
- [ ] Model comparison utilities
- [ ] Simulation testing framework
- [ ] Report generation (Jupyter → PDF/HTML)
- [ ] Parameter sensitivity analysis

### Phase 4: Advanced Models & Production Ready
**Timeline: 3-4 months**

#### 4.1 Complex Assessment Models
- [ ] Integrated assessment models
- [ ] Multi-species models
- [ ] Spatial models
- [ ] Tag-recapture models

#### 4.2 Performance & Scalability
- [ ] Parallel processing support
- [ ] Large dataset optimization
- [ ] Memory efficient operations
- [ ] Cloud deployment ready

#### 4.3 Community Features
- [ ] Model sharing/repository
- [ ] Documentation and tutorials
- [ ] Example datasets and case studies
- [ ] Workshop materials

## 🛠 Technical Architecture

### Core Components

```
PyADMB/
├── pyadmb/
│   ├── core/           # Core ADMB interface
│   ├── models/         # Pre-built model templates
│   ├── data/           # Data handling utilities
│   ├── diagnostics/    # Model diagnostics & ML integration
│   ├── plotting/       # Visualization tools
│   └── utils/          # Helper functions
├── examples/           # Example notebooks and scripts
├── tests/             # Test suite
└── docs/              # Documentation
```

### Dependencies

**Core Requirements:**
- Python >=3.8+
- ADMB >=13.0+
- pandas >= 1.3.0
- numpy >= 1.20.0
- matplotlib >= 3.3.0

**Optional (for enhanced features):**
- scikit-learn (ML diagnostics)
- seaborn (advanced plotting)
- jupyter (notebook integration)
- plotly (interactive plots)

## 📚 Usage Examples

### Basic Surplus Production Model
```python
import pandas as pd
from pyadmb import SurplusProductionModel

# Load data
catch_data = pd.read_csv('catch.csv')
survey_data = pd.read_csv('survey.csv')

# Create and configure model
model = SurplusProductionModel()
model.set_catch_data(catch_data, catch_col='catch', year_col='year')
model.set_survey_data(survey_data, index_col='cpue', year_col='year')

# Set priors
model.set_priors(
    r=(0.2, 0.8),      # Intrinsic growth rate
    K=(5000, 20000),   # Carrying capacity
    q=(0.0001, 0.01)   # Catchability coefficient
)

# Fit model
results = model.fit()

# Analyze results
print(results.reference_points)
results.plot_biomass_trajectory()
results.plot_residuals()
```

### Integration with Machine Learning
```python
from pyadmb.diagnostics import ResidualAnalysis
from sklearn.ensemble import RandomForestRegressor

# Analyze model residuals with ML
residual_analysis = ResidualAnalysis(results)
patterns = residual_analysis.detect_patterns(
    method=RandomForestRegressor(),
    features=['year', 'age', 'fleet']
)

# Identify potential model improvements
recommendations = residual_analysis.suggest_improvements()
print(recommendations)
```

## 🤝 Contributing

We welcome contributions from the fisheries and Python communities!

### Getting Started
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Install development dependencies (`pip install -e .[dev]`)
4. Make your changes
5. Add tests for new functionality
6. Submit a pull request

### Development Setup
```bash
git clone https://github.com/your-username/pyadmb.git
cd pyadmb
pip install -e .[dev]
pre-commit install
pytest tests/
```

## 📖 Documentation

- **User Guide**: Comprehensive tutorials and examples
- **API Reference**: Complete function and class documentation
- **Case Studies**: Real-world fisheries assessment examples
- **Best Practices**: Guidelines for effective stock assessment

## 🎓 Educational Resources

### Workshops & Tutorials
- Beginner's guide to stock assessment with PyADMB
- Advanced modeling techniques
- ML integration for stock assessment
- Comparative analysis: PyADMB vs traditional tools

### Example Datasets
- North Pacific groundfish stocks
- Atlantic tuna assessments
- Data-limited tropical fisheries
- Simulated populations for testing

## 🚧 Roadmap

### Version 0.1.0 (MVP)
- [ ] Basic surplus production models
- [ ] Simple catch-at-age models
- [ ] Core plotting functions
- [ ] Documentation and examples

### Version 0.2.0
- [ ] ML diagnostics integration
- [ ] Advanced plotting
- [ ] Model comparison tools
- [ ] Simulation framework

### Version 1.0.0
- [ ] Comprehensive model library
- [ ] Production-ready performance
- [ ] Full documentation
- [ ] Community adoption

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

## 📞 Contact

- **Issues & Bugs**: [GitHub Issues](https://github.com/halprez/pyadmb/issues)
- **Discussions**: [GitHub Discussions](https://github.com/halprez/pyadmb/discussions)

---

*PyADMB: Bringing fisheries stock assessment into the modern Python ecosystem*