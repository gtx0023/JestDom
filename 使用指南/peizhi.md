# 使用jest对vue项目进行单元测试 配置

```json
{
  "jest": {
    clearMocks: true,
    // 统计
    collectCoverage: true,
    collectCoverageFrom: ['**/*.{ts,vue}', '!**/node_modules/**'],
    // 测试范围文件
    "moduleFileExtensions": [
      "js",
      "jsx",
      "json",
      "vue",
      "ts",
      "tsx"
    ],
    "transform": {
      "^.+\\.vue$": "vue-jest",
      ".+\\.(css|styl|less|sass|scss|png|jpg|ttf|woff|woff2)$": "jest-transform-stub",
      "^.+\\.tsx?$": "ts-jest"
    },
    // 跳过测试部分
    coveragePathIgnorePatterns: [
      'node_modules'  
    ],
    // 解析别名
    "moduleNameMapper": {
      "^@/(.*)$": "<rootDir>/src/$1"
    },
    "snapshotSerializers": [
      "jest-serializer-vue"
    ],
    // 不设置 默认就好
    "testMatch": [
      "**/tests/unit/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx)"
    ],
    // 不设置 默认就好
    "testURL": "http://localhost/"
  }
}
```

