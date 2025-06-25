# NutriGenieVegAI - Comprehensive Project Documentation

## Table of Contents
- [Project Overview](#project-overview)
- [Core Features](#core-features)
- [Technologies & Tools](#technologies--tools)
- [Architecture](#architecture)
- [API Documentation](#api-documentation)
- [Setup & Installation](#setup--installation)
- [Usage Guide](#usage-guide)
- [Development Notes](#development-notes)

---

## Project Overview

**NutriGenieVegAI** is an AI-powered fitness recipe recommender system designed specifically for plant-based diets. It combines advanced nutrition science, machine learning, and comprehensive recipe databases to provide personalized meal recommendations that align with fitness goals and dietary preferences.

### Key Highlights
- **AI-Powered Recipe Generation**: Uses Mistral-7B-Instruct for intelligent recipe creation
- **Personalized Nutrition**: Calculates BMI, TDEE, and optimal macronutrient splits
- **Plant-Based Focus**: Specialized for vegetarian, vegan, and plant-based diets
- **Real-Time Analysis**: Live nutritional calculations and dietary compliance checking
- **Modern Architecture**: FastAPI backend with Streamlit frontend

---

## Core Features

### 1. Personalized Nutrition System

#### BMI & TDEE Calculation
- **Automatic BMI Computation**: Based on height and weight inputs
- **TDEE Calculation**: Uses Mifflin-St Jeor equation for accurate daily calorie needs
- **Activity Level Support**: 5 different activity multipliers (1.2 - 1.9)
- **Fitness Goal Targeting**: Deficit, maintenance, and bulking calculations

#### Macronutrient Optimization
```python
# Macro splits based on fitness goals:
Deficit:    40% protein, 40% carbs, 20% fat
Maintenance: 30% protein, 45% carbs, 25% fat  
Bulking:    30% protein, 50% carbs, 20% fat
```

#### Fiber Recommendations
- **Smart Fiber Calculation**: 14g per 1000 calories
- **Dietary Compliance**: Ensures adequate fiber intake for health

### 2. Dietary Preference Management

#### Supported Diet Types
- **High-Protein Vegetarian**: Optimized for muscle building
- **High-Protein Vegan**: Plant-based protein focus
- **Low-Carb Vegetarian**: Ketogenic-friendly options
- **Keto Vegetarian**: Strict low-carb plant-based
- **Athlete/Bodybuilder Plant-Based**: Performance-focused nutrition
- **Whole-Food Plant-Based (WFPB)**: Minimally processed foods
- **Fruitarian**: Fruit-focused diet

#### Allergen & Restriction Support
- **Common Allergens**: Gluten, dairy, nuts, soy, eggs, shellfish, fish
- **Dietary Restrictions**: Lacto-vegetarian, ovo-vegetarian, lacto-ovo vegetarian
- **Automatic Filtering**: Real-time allergen detection and avoidance

### 3. AI-Powered Recipe Generation

#### Mistral-7B-Instruct Integration
- **Advanced LLM**: 7B parameter instruction-tuned model
- **Nutritional Targeting**: Recipes generated to match specific calorie/macro targets
- **Ingredient Intelligence**: Smart ingredient parsing and measurement conversion
- **Recipe Variations**: AI-generated variations of existing recipes

#### Recipe Analysis Features
- **Nutritional Analysis**: AI-powered recipe evaluation
- **Improvement Suggestions**: Intelligent recommendations for better nutrition
- **Macro Optimization**: Suggestions for better macro balance

### 4. Recipe Database & Search

#### TheMealDB Integration
- **Extensive Database**: 500+ recipes from TheMealDB
- **Categorized Recipes**: Organized by cuisine, meal type, difficulty
- **Rich Metadata**: Complete recipe information with images

#### ChromaDB Vector Search
- **Semantic Search**: Fast similarity-based recipe retrieval
- **Embedding Storage**: Recipe content vectorization
- **Intelligent Caching**: Performance optimization with expiration
- **Real-time Updates**: Dynamic recipe database updates

### 5. Nutritional Analysis

#### USDA FoodData Central Integration
- **Comprehensive Database**: Complete nutritional information
- **Per-100g Values**: Standardized nutritional data
- **Ingredient Lookup**: Real-time nutritional value retrieval

#### Unit Conversion System
```python
# Supported conversions:
- Weight: g, kg, mg, lb, oz
- Volume: cup, tbsp, tsp
- Common: pinch, clove, slice, piece
- Sizes: large, medium, small
```

---

## Technologies & Tools

### Backend Technologies

#### Web Framework
- **FastAPI**: Modern, fast web framework for building APIs
- **Uvicorn**: ASGI server for running FastAPI applications
- **Pydantic**: Data validation and settings management

#### Database & ORM
- **SQLAlchemy**: Database ORM and migration support
- **Alembic**: Database migration tool
- **PostgreSQL**: Primary database (via psycopg2-binary)
- **ChromaDB**: Vector database for semantic search

### AI/ML Technologies

#### Core ML Framework
- **Transformers (Hugging Face)**: State-of-the-art NLP models
- **PyTorch**: Deep learning framework
- **Mistral-7B-Instruct**: 7B parameter instruction-tuned language model

#### Supporting Libraries
- **SentencePiece**: Tokenization for multilingual models
- **Einops**: Tensor operations for deep learning
- **Scikit-learn**: Machine learning utilities
- **Protobuf**: Data serialization

### Frontend Technologies

#### Web Application
- **Streamlit**: Rapid web application development
- **Custom CSS**: Modern, responsive design
- **Interactive Components**: Real-time form validation

#### Data Processing
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Requests**: HTTP library for API calls

### External APIs & Services

#### Recipe Data
- **TheMealDB API**: Free recipe database with 500+ recipes
- **USDA FoodData Central API**: Comprehensive nutritional database

#### Model Hosting
- **Hugging Face Model Hub**: Model hosting and distribution

### Development & Deployment

#### Environment Management
- **Python 3.x**: Primary programming language
- **Virtual Environment**: Isolated dependency management
- **Environment Variables**: Secure configuration management

#### Version Control & Deployment
- **Git**: Version control
- **Docker Support**: Containerization ready
- **Requirements.txt**: Dependency management

---

## Architecture

### Backend Architecture

```
FastAPI Application
├── Core Modules
│   ├── calculations.py (Nutrition math)
│   ├── llama_model.py (AI model interface)
│   ├── recipe_generator.py (Recipe creation logic)
│   └── embeddings.py (Vector operations)
├── Database Layer
│   ├── chroma_client.py (Vector database)
│   └── models.py (Data models)
├── API Clients
│   ├── meal_db_client.py (TheMealDB integration)
│   └── usda_client.py (Nutrition API)
└── Schemas
    └── recipe.py (Data validation)
```

### Frontend Architecture

```
Streamlit Application
├── User Profile Management
├── Nutrition Calculator
├── Recipe Recommendation Interface
├── Interactive Recipe Cards
└── Real-time API Status Monitoring
```

### Data Flow

```
User Input → Frontend → FastAPI Backend
    ↓
Nutrition Calculation → Recipe Search → AI Generation
    ↓
ChromaDB (Vector Search) + TheMealDB + USDA API
    ↓
Recipe Response → Frontend Display
```

---

## API Documentation

### Core Endpoints

#### 1. Nutrition Calculation
```http
POST /calculate-nutrition
```
**Purpose**: Calculate BMI, TDEE, target calories, and macro split
**Request Body**:
```json
{
  "height": 175.0,
  "weight": 70.0,
  "age": 25,
  "sex": "male",
  "activity_level": 1.55,
  "fitness_goal": "deficit",
  "dietary_preference": "high-protein vegetarian",
  "dietary_restrictions": ["gluten-free"]
}
```

#### 2. Recipe Generation
```http
POST /generate-recipe
```
**Purpose**: Generate AI-powered recipes based on preferences
**Request Body**:
```json
{
  "dietary_preference": "high-protein vegetarian",
  "dietary_restrictions": ["gluten-free"],
  "target_calories": 2000,
  "macro_split": {
    "protein": 200,
    "carbs": 200,
    "fat": 44,
    "fiber": 28
  }
}
```

#### 3. Recipe Recommendations
```http
POST /recommend-recipes
```
**Purpose**: Get personalized recipe recommendations
**Features**:
- Semantic search in ChromaDB
- Dietary restriction filtering
- Nutritional target matching
- Fallback to AI generation

#### 4. Recipe Variations
```http
POST /recipe-variations/{recipe_id}
```
**Purpose**: Generate variations of existing recipes
**Parameters**:
- `recipe_id`: ID of base recipe
- `num_variations`: Number of variations (default: 3)

#### 5. Recipe Analysis
```http
POST /analyze-recipe/{recipe_id}
```
**Purpose**: Analyze recipe nutrition and provide suggestions
**Response**:
```json
{
  "analysis": "Nutritional content analysis",
  "suggestions": ["suggestion1", "suggestion2"],
  "improved_macros": {
    "protein": 25,
    "carbs": 30,
    "fat": 15,
    "fiber": 8
  }
}
```

### Utility Endpoints

#### Health Check
```http
GET /health
```
**Purpose**: Check API health status
**Response**:
```json
{
  "status": "healthy",
  "timestamp": "2024-01-01T00:00:00Z",
  "version": "1.0.0"
}
```

#### Readiness Check
```http
GET /ready
```
**Purpose**: Check if service is ready to handle requests
**Response**:
```json
{
  "ready": true,
  "model_loaded": true,
  "chroma_initialized": true
}
```

---

## Setup & Installation

### Prerequisites
- Python 3.8+
- 12GB+ GPU VRAM (recommended for optimal performance)
- PostgreSQL database
- Git

### Installation Steps

#### 1. Clone Repository
```bash
git clone https://github.com/nikitakodkany/vegReciperRecommender.git
cd vegReciperRecommender
```

#### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

#### 3. Environment Setup
```bash
# Create .env file
cp .env.example .env

# Configure environment variables
DATABASE_URL=postgresql://user:password@localhost/nutrigenie
USDA_API_KEY=your_usda_api_key
```

#### 4. Database Setup
```bash
# Initialize database
alembic upgrade head
```

#### 5. Run Backend
```bash
cd backend/app
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

#### 6. Run Frontend
```bash
cd frontend/src
streamlit run app.py
```

### Configuration Options

#### Model Configuration
```python
# backend/app/core/llama_model.py
model_name = "mistralai/Mistral-7B-Instruct-v0.2"
torch_dtype = torch.float16  # For memory efficiency
device_map = "auto"  # Automatic GPU/CPU placement
```

#### ChromaDB Configuration
```python
# backend/app/db/chroma_client.py
persistent_client_path = "data/chroma"
collection_name = "recipes"
cache_expiry_minutes = 30
```

---

## Usage Guide

### Getting Started

#### 1. Access the Application
- Open browser to `http://localhost:8501`
- Check API status in sidebar

#### 2. Create Your Profile
- **Physical Metrics**: Height, weight, age, sex
- **Activity Level**: Choose from 5 activity levels
- **Fitness Goal**: Deficit, maintenance, or bulking
- **Dietary Preferences**: Select plant-based diet type
- **Restrictions**: Add allergens and dietary restrictions

#### 3. Get Recommendations
- Click "Get AI-Generated Recommendations"
- View nutritional profile and target macros
- Browse personalized recipe suggestions

### Advanced Features

#### Recipe Customization
- **Ingredient Preferences**: Specify preferred ingredients
- **Cuisine Types**: Choose preferred cuisines
- **Meal Types**: Breakfast, lunch, dinner, snacks
- **Time Constraints**: Set maximum prep/cook times

#### Nutritional Analysis
- **Macro Tracking**: Real-time macro calculations
- **Calorie Monitoring**: Daily calorie targets
- **Fiber Tracking**: Fiber intake monitoring
- **Allergen Alerts**: Automatic allergen detection

#### Recipe Management
- **Save Favorites**: Bookmark preferred recipes
- **Generate Variations**: Create recipe variations
- **Nutritional Analysis**: Get improvement suggestions
- **Export Recipes**: Save recipes for later use

### Best Practices

#### For Optimal Results
1. **Accurate Measurements**: Use precise height/weight measurements
2. **Realistic Activity Levels**: Choose appropriate activity multiplier
3. **Clear Dietary Goals**: Specify exact dietary preferences
4. **Regular Updates**: Update profile as goals change

#### Performance Tips
1. **GPU Usage**: Ensure sufficient VRAM for model loading
2. **Caching**: Leverage built-in caching for faster responses
3. **Batch Requests**: Group multiple recipe requests
4. **Offline Mode**: Use cached recipes when API unavailable

---

## Development Notes

### Code Structure

#### Backend Organization
```
backend/app/
├── main.py              # FastAPI application entry point
├── core/                # Core business logic
│   ├── calculations.py  # Nutrition calculations
│   ├── llama_model.py   # AI model interface
│   ├── recipe_generator.py # Recipe generation logic
│   └── embeddings.py    # Vector operations
├── db/                  # Database layer
│   ├── chroma_client.py # ChromaDB client
│   └── models.py        # Data models
├── clients/             # External API clients
│   ├── meal_db_client.py # TheMealDB integration
│   └── usda_client.py   # USDA API client
└── schemas/             # Data validation schemas
    └── recipe.py        # Recipe data models
```

#### Frontend Organization
```
frontend/src/
├── app.py              # Streamlit main application
├── components/         # Reusable UI components
├── utils/             # Utility functions
└── assets/            # Static assets
```

### Key Design Patterns

#### 1. Dependency Injection
- Modular client architecture
- Easy component replacement
- Testable code structure

#### 2. Caching Strategy
- Multi-level caching (memory + database)
- Intelligent cache invalidation
- Performance optimization

#### 3. Error Handling
- Comprehensive exception handling
- Graceful degradation
- User-friendly error messages

#### 4. Background Processing
- Non-blocking model loading
- Asynchronous recipe generation
- Real-time status updates

### Performance Considerations

#### Memory Management
- **Model Loading**: Lazy loading of large models
- **GPU Memory**: Efficient tensor operations
- **Cache Management**: Automatic cache cleanup

#### Scalability
- **Horizontal Scaling**: Stateless API design
- **Database Optimization**: Indexed queries
- **CDN Integration**: Static asset delivery

### Security Features

#### API Security
- **Input Validation**: Pydantic model validation
- **Rate Limiting**: Request throttling
- **CORS Configuration**: Cross-origin resource sharing

#### Data Protection
- **Environment Variables**: Secure configuration
- **API Key Management**: Secure API key storage
- **Input Sanitization**: XSS prevention

### Testing Strategy

#### Unit Testing
- **Core Functions**: Nutrition calculations
- **API Endpoints**: Request/response validation
- **Data Models**: Schema validation

#### Integration Testing
- **External APIs**: TheMealDB, USDA integration
- **Database Operations**: ChromaDB functionality
- **End-to-End**: Complete user workflows

### Deployment Considerations

#### Production Setup
- **Environment Variables**: Secure configuration
- **Database Migration**: Alembic migrations
- **Logging**: Structured logging
- **Monitoring**: Health checks and metrics

#### Containerization
- **Docker Support**: Multi-stage builds
- **Environment Isolation**: Containerized services
- **Resource Limits**: Memory and CPU constraints

---

## Contributing

### Development Setup
1. Fork the repository
2. Create feature branch
3. Implement changes
4. Add tests
5. Submit pull request

### Code Standards
- **Python**: PEP 8 compliance
- **Type Hints**: Full type annotation
- **Documentation**: Docstring coverage
- **Testing**: 90%+ test coverage

### Issue Reporting
- **Bug Reports**: Detailed reproduction steps
- **Feature Requests**: Clear use case description
- **Performance Issues**: Profiling data

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- **Mistral AI**: For the Mistral-7B-Instruct model
- **TheMealDB**: For the comprehensive recipe database
- **USDA**: For the nutritional data API
- **Hugging Face**: For model hosting and distribution
- **FastAPI**: For the modern web framework
- **Streamlit**: For the rapid frontend development

---

**NutriGenieVegAI** - Your AI-powered fitness companion for plant-based nutrition! 🌱💪 