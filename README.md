# Stephen Mburu

**Senior UI/UX Frontend Architect** • Nairobi, Kenya 🇰🇪

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/stephen-mburu)
[![Portfolio](https://img.shields.io/badge/Portfolio-000000?style=flat&logo=vercel&logoColor=white)](https://mac254.dev)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:mburustephen167@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat&logo=github&logoColor=white)](https://github.com/mac254)

---

## Code Portfolio

### 🎯 Custom React Hooks

```tsx
// useAsync - Custom hook for handling async operations
export const useAsync = <T>(asyncFunction: () => Promise<T>, deps: any[] = []) => {
  const [state, setState] = useState<{
    data: T | null;
    loading: boolean;
    error: Error | null;
  }>({
    data: null,
    loading: false,
    error: null,
  });

  const execute = useCallback(async () => {
    setState({ data: null, loading: true, error: null });
    try {
      const result = await asyncFunction();
      setState({ data: result, loading: false, error: null });
    } catch (error) {
      setState({ data: null, loading: false, error: error as Error });
    }
  }, deps);

  useEffect(() => {
    execute();
  }, [execute]);

  return { ...state, execute };
};

// useLocalStorage - Type-safe localStorage hook
export const useLocalStorage = <T>(key: string, initialValue: T) => {
  const [storedValue, setStoredValue] = useState<T>(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(`Error reading localStorage key "${key}":`, error);
      return initialValue;
    }
  });

  const setValue = (value: T | ((val: T) => T)) => {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(`Error setting localStorage key "${key}":`, error);
    }
  };

  return [storedValue, setValue] as const;
};
```

### 🛠️ Advanced Component Patterns

```tsx
// Higher-Order Component with TypeScript
export const withAuth = <P extends object>(
  Component: React.ComponentType<P>
) => {
  return (props: P) => {
    const { user, loading } = useAuth();
    
    if (loading) return <LoadingSpinner />;
    if (!user) return <Navigate to="/login" />;
    
    return <Component {...props} />;
  };
};

// Render Props Pattern
interface DataFetcherProps<T> {
  url: string;
  children: (data: {
    data: T | null;
    loading: boolean;
    error: Error | null;
    refetch: () => void;
  }) => React.ReactNode;
}

export const DataFetcher = <T,>({ url, children }: DataFetcherProps<T>) => {
  const { data, loading, error, execute } = useAsync(
    () => fetch(url).then(res => res.json()),
    [url]
  );

  return <>{children({ data, loading, error, refetch: execute })}</>;
};

// Compound Components
interface TabsContextType {
  activeTab: string;
  setActiveTab: (tab: string) => void;
}

const TabsContext = createContext<TabsContextType | null>(null);

export const Tabs = ({ children, defaultTab }: { children: React.ReactNode; defaultTab: string }) => {
  const [activeTab, setActiveTab] = useState(defaultTab);
  
  return (
    <TabsContext.Provider value={{ activeTab, setActiveTab }}>
      <div className="tabs-container">{children}</div>
    </TabsContext.Provider>
  );
};

Tabs.List = ({ children }: { children: React.ReactNode }) => (
  <div className="tabs-list">{children}</div>
);

Tabs.Tab = ({ value, children }: { value: string; children: React.ReactNode }) => {
  const context = useContext(TabsContext);
  if (!context) throw new Error('Tab must be used within Tabs');
  
  const { activeTab, setActiveTab } = context;
  
  return (
    <button
      className={`tab ${activeTab === value ? 'active' : ''}`}
      onClick={() => setActiveTab(value)}
    >
      {children}
    </button>
  );
};
```

### ⚡ Performance Optimizations

```tsx
// Virtual Scrolling Implementation
export const VirtualScrollList = <T,>({
  items,
  itemHeight,
  containerHeight,
  renderItem,
}: {
  items: T[];
  itemHeight: number;
  containerHeight: number;
  renderItem: (item: T, index: number) => React.ReactNode;
}) => {
  const [scrollTop, setScrollTop] = useState(0);
  const containerRef = useRef<HTMLDivElement>(null);

  const visibleStart = Math.floor(scrollTop / itemHeight);
  const visibleEnd = Math.min(
    visibleStart + Math.ceil(containerHeight / itemHeight),
    items.length - 1
  );

  const visibleItems = items.slice(visibleStart, visibleEnd + 1);

  const handleScroll = useCallback((e: React.UIEvent<HTMLDivElement>) => {
    setScrollTop(e.currentTarget.scrollTop);
  }, []);

  return (
    <div
      ref={containerRef}
      style={{ height: containerHeight, overflow: 'auto' }}
      onScroll={handleScroll}
    >
      <div style={{ height: items.length * itemHeight, position: 'relative' }}>
        {visibleItems.map((item, index) => (
          <div
            key={visibleStart + index}
            style={{
              position: 'absolute',
              top: (visibleStart + index) * itemHeight,
              height: itemHeight,
              width: '100%',
            }}
          >
            {renderItem(item, visibleStart + index)}
          </div>
        ))}
      </div>
    </div>
  );
};

// Debounced Search Hook
export const useDebounce = <T>(value: T, delay: number): T => {
  const [debouncedValue, setDebouncedValue] = useState<T>(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
};
```

### 🎨 Design System Components

```tsx
// Button Component with Variants
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'outline' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  loading?: boolean;
  leftIcon?: React.ReactNode;
  rightIcon?: React.ReactNode;
}

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  (
    {
      variant = 'primary',
      size = 'md',
      loading = false,
      leftIcon,
      rightIcon,
      children,
      className,
      disabled,
      ...props
    },
    ref
  ) => {
    const baseClasses = 'inline-flex items-center justify-center font-medium transition-colors';
    
    const variants = {
      primary: 'bg-blue-600 text-white hover:bg-blue-700 focus:ring-blue-500',
      secondary: 'bg-gray-200 text-gray-900 hover:bg-gray-300 focus:ring-gray-500',
      outline: 'border border-gray-300 text-gray-700 hover:bg-gray-50 focus:ring-gray-500',
      ghost: 'text-gray-700 hover:bg-gray-100 focus:ring-gray-500',
    };

    const sizes = {
      sm: 'h-8 px-3 text-sm',
      md: 'h-10 px-4 text-sm',
      lg: 'h-12 px-6 text-base',
    };

    return (
      <button
        ref={ref}
        className={cn(
          baseClasses,
          variants[variant],
          sizes[size],
          'focus:outline-none focus:ring-2 focus:ring-offset-2',
          disabled && 'opacity-50 cursor-not-allowed',
          className
        )}
        disabled={disabled || loading}
        {...props}
      >
        {loading && <Spinner className="w-4 h-4 mr-2" />}
        {!loading && leftIcon && <span className="mr-2">{leftIcon}</span>}
        {children}
        {!loading && rightIcon && <span className="ml-2">{rightIcon}</span>}
      </button>
    );
  }
);
```

### 🔧 State Management

```tsx
// Custom Context + Reducer Pattern
interface AppState {
  user: User | null;
  theme: 'light' | 'dark';
  notifications: Notification[];
  loading: boolean;
}

type AppAction =
  | { type: 'SET_USER'; payload: User | null }
  | { type: 'SET_THEME'; payload: 'light' | 'dark' }
  | { type: 'ADD_NOTIFICATION'; payload: Notification }
  | { type: 'REMOVE_NOTIFICATION'; payload: string }
  | { type: 'SET_LOADING'; payload: boolean };

const appReducer = (state: AppState, action: AppAction): AppState => {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    case 'SET_THEME':
      return { ...state, theme: action.payload };
    case 'ADD_NOTIFICATION':
      return {
        ...state,
        notifications: [...state.notifications, action.payload],
      };
    case 'REMOVE_NOTIFICATION':
      return {
        ...state,
        notifications: state.notifications.filter(n => n.id !== action.payload),
      };
    case 'SET_LOADING':
      return { ...state, loading: action.payload };
    default:
      return state;
  }
};

// Context Provider
export const AppProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [state, dispatch] = useReducer(appReducer, {
    user: null,
    theme: 'light',
    notifications: [],
    loading: false,
  });

  const actions = {
    setUser: (user: User | null) => dispatch({ type: 'SET_USER', payload: user }),
    setTheme: (theme: 'light' | 'dark') => dispatch({ type: 'SET_THEME', payload: theme }),
    addNotification: (notification: Notification) => 
      dispatch({ type: 'ADD_NOTIFICATION', payload: notification }),
    removeNotification: (id: string) => 
      dispatch({ type: 'REMOVE_NOTIFICATION', payload: id }),
    setLoading: (loading: boolean) => dispatch({ type: 'SET_LOADING', payload: loading }),
  };

  return (
    <AppContext.Provider value={{ state, actions }}>
      {children}
    </AppContext.Provider>
  );
};
```

### 🧪 Testing Utilities

```tsx
// Custom Testing Library Utils
export const renderWithProviders = (
  ui: React.ReactElement,
  {
    preloadedState = {},
    store = setupStore(preloadedState),
    ...renderOptions
  }: ExtendedRenderOptions = {}
) => {
  function Wrapper({ children }: PropsWithChildren<{}>): JSX.Element {
    return (
      <Provider store={store}>
        <BrowserRouter>
          <ThemeProvider theme={theme}>
            {children}
          </ThemeProvider>
        </BrowserRouter>
      </Provider>
    );
  }

  return { store, ...render(ui, { wrapper: Wrapper, ...renderOptions }) };
};

// Mock API Handlers
export const handlers = [
  rest.get('/api/users', (req, res, ctx) => {
    return res(ctx.json({ users: mockUsers }));
  }),
  
  rest.post('/api/users', (req, res, ctx) => {
    return res(ctx.json({ user: mockUser }));
  }),
  
  rest.get('/api/users/:id', (req, res, ctx) => {
    const { id } = req.params;
    const user = mockUsers.find(u => u.id === id);
    return user ? res(ctx.json({ user })) : res(ctx.status(404));
  }),
];
```

### 🔄 API Integration

```tsx
// React Query Integration
export const useUser = (id: string) => {
  return useQuery({
    queryKey: ['user', id],
    queryFn: () => api.users.getById(id),
    enabled: !!id,
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
};

export const useUpdateUser = () => {
  const queryClient = useQueryClient();
  
  return useMutation({
    mutationFn: (user: UpdateUserDto) => api.users.update(user.id, user),
    onSuccess: (data) => {
      queryClient.setQueryData(['user', data.id], data);
      queryClient.invalidateQueries({ queryKey: ['users'] });
    },
  });
};

// Custom API Client
class ApiClient {
  private baseURL: string;
  
  constructor(baseURL: string) {
    this.baseURL = baseURL;
  }

  private async request<T>(
    endpoint: string,
    options: RequestInit = {}
  ): Promise<T> {
    const url = `${this.baseURL}${endpoint}`;
    const config: RequestInit = {
      headers: {
        'Content-Type': 'application/json',
        ...options.headers,
      },
      ...options,
    };

    const response = await fetch(url, config);
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return response.json();
  }

  get<T>(endpoint: string) {
    return this.request<T>(endpoint);
  }

  post<T>(endpoint: string, data: any) {
    return this.request<T>(endpoint, {
      method: 'POST',
      body: JSON.stringify(data),
    });
  }

  put<T>(endpoint: string, data: any) {
    return this.request<T>(endpoint, {
      method: 'PUT',
      body: JSON.stringify(data),
    });
  }

  delete<T>(endpoint: string) {
    return this.request<T>(endpoint, {
      method: 'DELETE',
    });
  }
}
```

### 🌐 Build Configuration

```javascript
// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  entry: './src/index.tsx',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js',
    clean: true,
  },
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
      {
        test: /\.scss$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          'sass-loader',
        ],
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
    new MiniCssExtractPlugin({
      filename: '[name].[contenthash].css',
    }),
  ],
  optimization: {
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all',
        },
      },
    },
  },
};
```

---

## 📊 GitHub Stats

<div align="center">
  
![Stephen's GitHub Stats](https://github-readme-stats.vercel.app/api?username=mac254&show_icons=true&theme=vue-dark&hide_border=true&include_all_commits=true)

![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=mac254&layout=compact&theme=vue-dark&hide_border=true)

</div>

---

## 🚀 Featured Projects

### [KenyaTech Platform](https://github.com/mac254/kenyatech)
**Tech Stack:** React, TypeScript, Next.js, PostgreSQL, Tailwind CSS

A comprehensive platform connecting Kenyan developers with global opportunities. Features include developer profiles, job matching algorithms, and community forums.

### [Design System Library](https://github.com/mac254/ui-component-library)
**Tech Stack:** React, TypeScript, Storybook, SCSS, Jest

Enterprise-grade component library with 50+ accessible components, comprehensive documentation, and 95% test coverage.

### [Real-time Analytics Dashboard](https://github.com/mac254/react-dashboard)
**Tech Stack:** React, Redux, WebSocket, Chart.js, Material-UI

Business intelligence dashboard with real-time data visualization, customizable widgets, and advanced filtering capabilities.

---

## 🔗 Connect & Collaborate

- 💼 **LinkedIn:** [stephen-mburu](https://linkedin.com/in/stephen-mburu)
- 🌐 **Portfolio:** [mac254.dev](https://mac254.dev)
- 📧 **Email:** [mburustephen167@gmail.com](mailto:mburustephen167@gmail.com)
- 📅 **Schedule:** [Book a meeting](https://calendly.com/stephen-mburu)

---

<div align="center">

![Profile Views](https://komarev.com/ghpvc/?username=mac254&color=blueviolet&style=flat)
[![GitHub followers](https://img.shields.io/github/followers/mac254?label=Followers&style=social)](https://github.com/mac254)

*"Code is like humor. When you have to explain it, it's bad."* - Cory House

</div>
