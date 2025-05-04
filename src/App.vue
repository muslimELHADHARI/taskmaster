<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900 transition-colors duration-300">
    <!-- Mobile Header -->
    <header class="lg:hidden bg-white dark:bg-gray-800 shadow-sm py-4 px-6 flex items-center justify-between">
      <div class="flex items-center">
        <button @click="isSidebarOpen = !isSidebarOpen" class="mr-4 text-gray-500 dark:text-gray-400">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        </button>
        <h1 class="text-xl font-bold text-gray-800 dark:text-white">{{ pageTitle }}</h1>
      </div>
      <div class="flex items-center space-x-3">
        <button @click="toggleDarkMode" class="text-gray-500 dark:text-gray-400">
          <svg v-if="isDarkMode" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
            stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
          </svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
            stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
          </svg>
        </button>
        <div class="relative">
          <button @click="isProfileMenuOpen = !isProfileMenuOpen"
            class="h-8 w-8 rounded-full bg-emerald-500 flex items-center justify-center text-white font-medium">
            {{ userInitials }}
          </button>
          <div v-if="isProfileMenuOpen"
            class="absolute right-0 mt-2 w-48 bg-white dark:bg-gray-800 rounded-md shadow-lg py-1 z-10">
            <a href="#" @click.prevent="changePage('settings')"
              class="block px-4 py-2 text-sm text-gray-700 dark:text-gray-200 hover:bg-gray-100 dark:hover:bg-gray-700">Settings</a>
            <a href="#"
              class="block px-4 py-2 text-sm text-gray-700 dark:text-gray-200 hover:bg-gray-100 dark:hover:bg-gray-700">Logout</a>
          </div>
        </div>
      </div>
    </header>

    <div class="flex h-screen pt-0 lg:pt-0 overflow-hidden">
      <!-- Sidebar -->
      <aside
        class="fixed lg:static inset-y-0 left-0 z-50 w-64 bg-white dark:bg-gray-800 shadow-lg transform transition-transform duration-300 ease-in-out"
        :class="isSidebarOpen ? 'translate-x-0' : '-translate-x-full lg:translate-x-0'">
        <div class="flex flex-col h-full">
          <!-- Sidebar Header -->
          <div class="p-4 border-b dark:border-gray-700">
            <div class="flex items-center justify-between">
              <div class="flex items-center space-x-2">
                <div class="h-8 w-8 rounded-md bg-emerald-500 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
                  </svg>
                </div>
                <h1 class="text-xl font-bold text-gray-800 dark:text-white">TaskMaster</h1>
              </div>
              <button @click="isSidebarOpen = false" class="lg:hidden text-gray-500 dark:text-gray-400">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                </svg>
              </button>
            </div>
          </div>

          <!-- Navigation -->
          <nav class="flex-1 px-2 py-4 space-y-1 overflow-y-auto">
            <a href="#" @click.prevent="changePage('dashboard')"
              class="flex items-center px-4 py-3 rounded-md transition-colors duration-200"
              :class="currentPage === 'dashboard' ? 'bg-emerald-50 dark:bg-emerald-900/20 text-emerald-600 dark:text-emerald-400' : 'text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700'">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
              </svg>
              Dashboard
            </a>
            <a href="#" @click.prevent="changePage('tasks')"
              class="flex items-center px-4 py-3 rounded-md transition-colors duration-200"
              :class="currentPage === 'tasks' ? 'bg-emerald-50 dark:bg-emerald-900/20 text-emerald-600 dark:text-emerald-400' : 'text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700'">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2M9 12l2 2 4-4" />
              </svg>
              Tasks
            </a>
            <a href="#" @click.prevent="changePage('analytics')"
              class="flex items-center px-4 py-3 rounded-md transition-colors duration-200"
              :class="currentPage === 'analytics' ? 'bg-emerald-50 dark:bg-emerald-900/20 text-emerald-600 dark:text-emerald-400' : 'text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700'">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
              </svg>
              Analytics
            </a>
            <a href="#" @click.prevent="changePage('settings')"
              class="flex items-center px-4 py-3 rounded-md transition-colors duration-200"
              :class="currentPage === 'settings' ? 'bg-emerald-50 dark:bg-emerald-900/20 text-emerald-600 dark:text-emerald-400' : 'text-gray-600 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700'">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              Settings
            </a>
          </nav>

          <!-- User Profile -->
          <div class="p-4 border-t dark:border-gray-700">
            <div class="flex items-center">
              <div
                class="h-10 w-10 rounded-full bg-emerald-500 flex items-center justify-center text-white font-medium">
                {{ userInitials }}
              </div>
              <div class="ml-3">
                <p class="text-sm font-medium text-gray-800 dark:text-white">{{ userName }}</p>
                <p class="text-xs text-gray-500 dark:text-gray-400">{{ userEmail }}</p>
              </div>
            </div>
          </div>
        </div>
      </aside>

      <!-- Main Content -->
      <main class="flex-1 overflow-y-auto p-4 lg:p-8">
        <!-- Dashboard Page -->
        <div v-if="currentPage === 'dashboard'" class="animate-fadeIn">
          <div class="hidden lg:flex items-center justify-between mb-8">
            <h1 class="text-2xl font-bold text-gray-800 dark:text-white">Dashboard</h1>
            <div class="flex items-center space-x-4">
              <button @click="toggleDarkMode"
                class="p-2 rounded-full bg-gray-100 dark:bg-gray-700 text-gray-500 dark:text-gray-400">
                <svg v-if="isDarkMode" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none"
                  viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                </svg>
                <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                </svg>
              </button>
            </div>
          </div>

          <!-- Dashboard Content -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 flex items-center">
              <div
                class="h-12 w-12 rounded-lg bg-emerald-100 dark:bg-emerald-900/30 flex items-center justify-center text-emerald-600 dark:text-emerald-400 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
                </svg>
              </div>
              <div>
                <p class="text-sm text-gray-500 dark:text-gray-400">Total Tasks</p>
                <p class="text-2xl font-bold text-gray-800 dark:text-white">{{ tasks.length }}</p>
              </div>
            </div>
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 flex items-center">
              <div
                class="h-12 w-12 rounded-lg bg-blue-100 dark:bg-blue-900/30 flex items-center justify-center text-blue-600 dark:text-blue-400 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <p class="text-sm text-gray-500 dark:text-gray-400">Pending Tasks</p>
                <p class="text-2xl font-bold text-gray-800 dark:text-white">{{ pendingTasksCount }}</p>
              </div>
            </div>
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 flex items-center">
              <div
                class="h-12 w-12 rounded-lg bg-green-100 dark:bg-green-900/30 flex items-center justify-center text-green-600 dark:text-green-400 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <p class="text-sm text-gray-500 dark:text-gray-400">Completed Tasks</p>
                <p class="text-2xl font-bold text-gray-800 dark:text-white">{{ completedTasksCount }}</p>
              </div>
            </div>
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 flex items-center">
              <div
                class="h-12 w-12 rounded-lg bg-red-100 dark:bg-red-900/30 flex items-center justify-center text-red-600 dark:text-red-400 mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <p class="text-sm text-gray-500 dark:text-gray-400">Overdue Tasks</p>
                <p class="text-2xl font-bold text-gray-800 dark:text-white">{{ overdueTasksCount }}</p>
              </div>
            </div>
          </div>

          <!-- Recent Tasks -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 mb-8">
            <div class="flex items-center justify-between mb-6">
              <h2 class="text-lg font-bold text-gray-800 dark:text-white">Recent Tasks</h2>
              <button @click="changePage('tasks')"
                class="text-sm text-emerald-600 dark:text-emerald-400 hover:underline">View All</button>
            </div>
            <div class="space-y-4">
              <div v-for="(task, index) in recentTasks" :key="index"
                class="flex items-center p-3 rounded-lg hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-colors">
                <input type="checkbox" :checked="task.completed" @change="toggleComplete(task)"
                  class="h-5 w-5 rounded border-gray-300 text-emerald-600 focus:ring-emerald-500 mr-4" />
                <div class="flex-1">
                  <p :class="{ 'line-through text-gray-500': task.completed }"
                    class="font-medium text-gray-800 dark:text-white">{{ task.title }}</p>
                  <p class="text-sm text-gray-500 dark:text-gray-400">{{ formatDate(task.dueDate) }}</p>
                </div>
                <div class="flex items-center">
                  <span class="text-xs px-2 py-1 rounded-full mr-2" :class="{
                    'bg-emerald-100 text-emerald-800 dark:bg-emerald-900/30 dark:text-emerald-400': task.priority === 'low',
                    'bg-yellow-100 text-yellow-800 dark:bg-yellow-900/30 dark:text-yellow-400': task.priority === 'medium',
                    'bg-red-100 text-red-800 dark:bg-red-900/30 dark:text-red-400': task.priority === 'high'
                  }">
                    {{ task.priority }}
                  </span>
                  <span
                    class="text-xs px-2 py-1 rounded-full bg-gray-100 text-gray-800 dark:bg-gray-700 dark:text-gray-300">
                    {{ task.category }}
                  </span>
                </div>
              </div>
              <div v-if="recentTasks.length === 0" class="text-center py-4">
                <p class="text-gray-500 dark:text-gray-400">No tasks found. Add a new task to get started.</p>
              </div>
            </div>
          </div>

          <!-- Task Categories -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Tasks by Category</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
              <div v-for="(count, category) in tasksByCategory" :key="category"
                class="bg-gray-50 dark:bg-gray-700/50 rounded-lg p-4">
                <div class="flex items-center justify-between">
                  <p class="font-medium text-gray-800 dark:text-white capitalize">{{ category }}</p>
                  <p class="text-lg font-bold text-emerald-600 dark:text-emerald-400">{{ count }}</p>
                </div>
                <div class="mt-2 h-2 bg-gray-200 dark:bg-gray-600 rounded-full overflow-hidden">
                  <div class="h-full bg-emerald-500 rounded-full"
                    :style="{ width: `${(count / tasks.length) * 100}%` }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Tasks Page -->
        <div v-if="currentPage === 'tasks'" class="animate-fadeIn">
          <div class="hidden lg:flex items-center justify-between mb-8">
            <h1 class="text-2xl font-bold text-gray-800 dark:text-white">Tasks</h1>
          </div>

          <!-- Add Task Form -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 mb-8">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-4">Add New Task</h2>
            <div class="flex flex-col md:flex-row gap-4 mb-4">
              <div class="flex-grow">
                <input v-model="newTask.title" @keyup.enter="addTask" type="text" placeholder="What needs to be done?"
                  class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white" />
              </div>
              <button @click="addTask"
                class="px-4 py-2 bg-emerald-600 text-white rounded-lg hover:bg-emerald-700 transition-colors">
                Add Task
              </button>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
              <!-- Category Selection -->
              <div>
                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Category</label>
                <select v-model="newTask.category"
                  class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white">
                  <option value="work">Work</option>
                  <option value="personal">Personal</option>
                  <option value="shopping">Shopping</option>
                  <option value="health">Health</option>
                  <option value="other">Other</option>
                </select>
              </div>

              <!-- Priority Selection -->
              <div>
                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Priority</label>
                <select v-model="newTask.priority"
                  class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white">
                  <option value="low">Low</option>
                  <option value="medium">Medium</option>
                  <option value="high">High</option>
                </select>
              </div>

              <!-- Due Date Selection -->
              <div>
                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Due Date</label>
                <input v-model="newTask.dueDate" type="date"
                  class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white" />
              </div>
            </div>
          </div>

          <!-- Filters and Search -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 mb-8">
            <div class="flex flex-col md:flex-row gap-4">
              <div class="flex-grow">
                <input v-model="searchQuery" type="text" placeholder="Search tasks..."
                  class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white" />
              </div>

              <div class="flex flex-wrap gap-2">
                <select v-model="filterStatus"
                  class="px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white">
                  <option value="all">All Status</option>
                  <option value="active">Active</option>
                  <option value="completed">Completed</option>
                </select>

                <select v-model="filterCategory"
                  class="px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white">
                  <option value="all">All Categories</option>
                  <option value="work">Work</option>
                  <option value="personal">Personal</option>
                  <option value="shopping">Shopping</option>
                  <option value="health">Health</option>
                  <option value="other">Other</option>
                </select>

                <select v-model="filterPriority"
                  class="px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white">
                  <option value="all">All Priorities</option>
                  <option value="low">Low</option>
                  <option value="medium">Medium</option>
                  <option value="high">High</option>
                </select>
              </div>
            </div>
          </div>

          <!-- Task List -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6">
            <div class="flex justify-between items-center mb-6">
              <h2 class="text-lg font-bold text-gray-800 dark:text-white">Task List</h2>
              <div class="flex items-center gap-4">
                <span class="text-sm text-gray-500 dark:text-gray-400">
                  {{ filteredTasks.length }} tasks ({{ completedTasksCount }} completed)
                </span>
                <button @click="clearCompleted"
                  class="text-sm text-red-600 dark:text-red-400 hover:text-red-800 dark:hover:text-red-300"
                  :disabled="completedTasksCount === 0">
                  Clear completed
                </button>
              </div>
            </div>

            <div v-if="filteredTasks.length > 0" class="space-y-4">
              <div v-for="(task, index) in filteredTasks" :key="index"
                class="p-4 border dark:border-gray-700 rounded-lg hover:shadow-md transition-shadow" :class="{
                  'bg-gray-50 dark:bg-gray-700/50': task.completed,
                  'bg-white dark:bg-gray-800': !task.completed,
                  'border-emerald-200 dark:border-emerald-900/30': !task.completed && task.priority === 'low',
                  'border-yellow-200 dark:border-yellow-900/30': !task.completed && task.priority === 'medium',
                  'border-red-200 dark:border-red-900/30': !task.completed && task.priority === 'high'
                }">
                <div class="flex items-start gap-3">
                  <!-- Checkbox -->
                  <div class="pt-1">
                    <input type="checkbox" :checked="task.completed" @change="toggleComplete(task)"
                      class="h-5 w-5 rounded border-gray-300 dark:border-gray-600 text-emerald-600 focus:ring-emerald-500" />
                  </div>

                  <!-- Task Content -->
                  <div class="flex-grow">
                    <!-- Task Title -->
                    <div v-if="editingTask !== task" class="flex items-center gap-2 flex-wrap">
                      <span :class="{ 'line-through text-gray-500 dark:text-gray-400': task.completed }"
                        class="text-lg font-medium text-gray-800 dark:text-white">
                        {{ task.title }}
                      </span>

                      <!-- Priority Badge -->
                      <span class="text-xs px-2 py-1 rounded-full" :class="{
                        'bg-emerald-100 text-emerald-800 dark:bg-emerald-900/30 dark:text-emerald-400': task.priority === 'low',
                        'bg-yellow-100 text-yellow-800 dark:bg-yellow-900/30 dark:text-yellow-400': task.priority === 'medium',
                        'bg-red-100 text-red-800 dark:bg-red-900/30 dark:text-red-400': task.priority === 'high'
                      }">
                        {{ task.priority }}
                      </span>

                      <!-- Category Badge -->
                      <span
                        class="text-xs px-2 py-1 rounded-full bg-gray-100 text-gray-800 dark:bg-gray-700 dark:text-gray-300">
                        {{ task.category }}
                      </span>
                    </div>

                    <!-- Edit Form -->
                    <div v-else class="flex items-center gap-2">
                      <input v-model="editedTitle" @keyup.enter="saveEdit" @keyup.esc="cancelEdit" type="text"
                        class="flex-grow px-2 py-1 border border-gray-300 dark:border-gray-600 rounded-md focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white" />
                      <button @click="saveEdit"
                        class="text-emerald-600 dark:text-emerald-400 hover:text-emerald-800 dark:hover:text-emerald-300">Save</button>
                      <button @click="cancelEdit"
                        class="text-gray-600 dark:text-gray-400 hover:text-gray-800 dark:hover:text-gray-300">Cancel</button>
                    </div>

                    <!-- Due Date -->
                    <div v-if="task.dueDate" class="text-sm text-gray-600 dark:text-gray-400 mt-1">
                      Due: {{ formatDate(task.dueDate) }}
                      <span v-if="isOverdue(task)" class="text-red-600 dark:text-red-400 ml-2">
                        (Overdue)
                      </span>
                    </div>
                  </div>

                  <!-- Action Buttons -->
                  <div class="flex gap-2">
                    <button v-if="editingTask !== task" @click="startEdit(task)"
                      class="text-gray-600 dark:text-gray-400 hover:text-gray-800 dark:hover:text-gray-300">
                      Edit
                    </button>
                    <button @click="deleteTask(task)"
                      class="text-red-600 dark:text-red-400 hover:text-red-800 dark:hover:text-red-300">
                      Delete
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <!-- Empty State -->
            <div v-else class="text-center py-10">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 mx-auto text-gray-400 dark:text-gray-600 mb-4"
                fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
              </svg>
              <p class="text-gray-500 dark:text-gray-400">No tasks found. Add a new task or adjust your filters.</p>
            </div>
          </div>
        </div>

        <!-- Analytics Page -->
        <div v-if="currentPage === 'analytics'" class="animate-fadeIn">
          <div class="hidden lg:flex items-center justify-between mb-8">
            <h1 class="text-2xl font-bold text-gray-800 dark:text-white">Analytics</h1>
          </div>

          <!-- Task Completion Rate -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 mb-8">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Task Completion Rate</h2>
            <div class="flex items-center justify-center">
              <div class="relative h-48 w-48">
                <svg class="h-full w-full" viewBox="0 0 100 100">
                  <!-- Background circle -->
                  <circle cx="50" cy="50" r="40" fill="none" stroke="#e5e7eb" stroke-width="10"
                    class="dark:stroke-gray-700" />
                  <!-- Progress circle -->
                  <circle cx="50" cy="50" r="40" fill="none"
                    :stroke="completionRate > 75 ? '#10b981' : completionRate > 50 ? '#3b82f6' : '#ef4444'"
                    stroke-width="10" stroke-dasharray="251.2"
                    :stroke-dashoffset="251.2 - (251.2 * completionRate) / 100" transform="rotate(-90 50 50)" />
                </svg>
                <div class="absolute inset-0 flex items-center justify-center">
                  <div class="text-center">
                    <p class="text-3xl font-bold text-gray-800 dark:text-white">{{ Math.round(completionRate) }}%</p>
                    <p class="text-sm text-gray-500 dark:text-gray-400">Completed</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Task Distribution -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-8">
            <!-- Tasks by Category -->
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6">
              <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Tasks by Category</h2>
              <div class="space-y-4">
                <div v-for="(count, category) in tasksByCategory" :key="category" class="flex items-center">
                  <div class="w-32 capitalize text-gray-800 dark:text-white font-medium">{{ category }}</div>
                  <div class="flex-1">
                    <div class="h-4 bg-gray-100 dark:bg-gray-700 rounded-full overflow-hidden">
                      <div class="h-full bg-emerald-500 rounded-full"
                        :style="{ width: `${(count / tasks.length) * 100}%` }"></div>
                    </div>
                  </div>
                  <div class="w-12 text-right text-gray-800 dark:text-white font-medium">{{ count }}</div>
                </div>
              </div>
            </div>

            <!-- Tasks by Priority -->
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6">
              <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Tasks by Priority</h2>
              <div class="space-y-4">
                <div v-for="(count, priority) in tasksByPriority" :key="priority" class="flex items-center">
                  <div class="w-32 capitalize text-gray-800 dark:text-white font-medium">{{ priority }}</div>
                  <div class="flex-1">
                    <div class="h-4 bg-gray-100 dark:bg-gray-700 rounded-full overflow-hidden">
                      <div class="h-full rounded-full" :class="{
                        'bg-emerald-500': priority === 'low',
                        'bg-yellow-500': priority === 'medium',
                        'bg-red-500': priority === 'high'
                      }" :style="{ width: `${(count / tasks.length) * 100}%` }"></div>
                    </div>
                  </div>
                  <div class="w-12 text-right text-gray-800 dark:text-white font-medium">{{ count }}</div>
                </div>
              </div>
            </div>
          </div>

          <!-- Task Completion Timeline -->
          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Task Activity</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
              <div>
                <h3 class="text-md font-medium text-gray-800 dark:text-white mb-4">Recently Completed</h3>
                <div class="space-y-4">
                  <div v-for="(task, index) in recentlyCompletedTasks" :key="index"
                    class="flex items-center p-3 rounded-lg bg-gray-50 dark:bg-gray-700/50">
                    <div
                      class="h-8 w-8 rounded-full bg-green-100 dark:bg-green-900/30 flex items-center justify-center text-green-600 dark:text-green-400 mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24"
                        stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                      </svg>
                    </div>
                    <div>
                      <p class="font-medium text-gray-800 dark:text-white">{{ task.title }}</p>
                      <p class="text-xs text-gray-500 dark:text-gray-400">Completed on {{ formatDate(task.completedAt)
                        }}</p>
                    </div>
                  </div>
                  <div v-if="recentlyCompletedTasks.length === 0" class="text-center py-4">
                    <p class="text-gray-500 dark:text-gray-400">No completed tasks yet.</p>
                  </div>
                </div>
              </div>
              <div>
                <h3 class="text-md font-medium text-gray-800 dark:text-white mb-4">Upcoming Due Dates</h3>
                <div class="space-y-4">
                  <div v-for="(task, index) in upcomingTasks" :key="index"
                    class="flex items-center p-3 rounded-lg bg-gray-50 dark:bg-gray-700/50">
                    <div
                      class="h-8 w-8 rounded-full bg-blue-100 dark:bg-blue-900/30 flex items-center justify-center text-blue-600 dark:text-blue-400 mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24"
                        stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                          d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                    </div>
                    <div>
                      <p class="font-medium text-gray-800 dark:text-white">{{ task.title }}</p>
                      <p class="text-xs text-gray-500 dark:text-gray-400">Due on {{ formatDate(task.dueDate) }}</p>
                    </div>
                  </div>
                  <div v-if="upcomingTasks.length === 0" class="text-center py-4">
                    <p class="text-gray-500 dark:text-gray-400">No upcoming tasks.</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Settings Page -->
        <div v-if="currentPage === 'settings'" class="animate-fadeIn">
          <div class="hidden lg:flex items-center justify-between mb-8">
            <h1 class="text-2xl font-bold text-gray-800 dark:text-white">Settings</h1>
          </div>

          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 mb-8">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Appearance</h2>
            <div class="flex items-center justify-between p-4 bg-gray-50 dark:bg-gray-700/50 rounded-lg">
              <div>
                <p class="font-medium text-gray-800 dark:text-white">Dark Mode</p>
                <p class="text-sm text-gray-500 dark:text-gray-400">Toggle between light and dark theme</p>
              </div>
              <button @click="toggleDarkMode" class="relative inline-flex h-6 w-11 items-center rounded-full"
                :class="isDarkMode ? 'bg-emerald-600' : 'bg-gray-200 dark:bg-gray-700'">
                <span class="inline-block h-4 w-4 transform rounded-full bg-white transition"
                  :class="isDarkMode ? 'translate-x-6' : 'translate-x-1'"></span>
              </button>
            </div>
          </div>

          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6 mb-8">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">User Profile</h2>
            <div class="space-y-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Name</label>
                <input v-model="userName" type="text"
                  class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white" />
              </div>
              <div>
                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Email</label>
                <input v-model="userEmail" type="email"
                  class="w-full px-4 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-emerald-500 bg-white dark:bg-gray-700 text-gray-800 dark:text-white" />
              </div>
              <button class="px-4 py-2 bg-emerald-600 text-white rounded-lg hover:bg-emerald-700 transition-colors">
                Save Profile
              </button>
            </div>
          </div>

          <div class="bg-white dark:bg-gray-800 rounded-xl shadow-sm p-6">
            <h2 class="text-lg font-bold text-gray-800 dark:text-white mb-6">Data Management</h2>
            <div class="space-y-4">
              <div class="flex items-center justify-between p-4 bg-gray-50 dark:bg-gray-700/50 rounded-lg">
                <div>
                  <p class="font-medium text-gray-800 dark:text-white">Export Data</p>
                  <p class="text-sm text-gray-500 dark:text-gray-400">Download all your tasks as JSON</p>
                </div>
                <button @click="exportData"
                  class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                  Export
                </button>
              </div>
              <div class="flex items-center justify-between p-4 bg-gray-50 dark:bg-gray-700/50 rounded-lg">
                <div>
                  <p class="font-medium text-gray-800 dark:text-white">Clear All Data</p>
                  <p class="text-sm text-gray-500 dark:text-gray-400">Remove all tasks and reset the application</p>
                </div>
                <button @click="clearAllData"
                  class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition-colors">
                  Clear Data
                </button>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>

    <!-- Floating Action Button (Mobile) -->
    <button v-if="currentPage === 'tasks'" @click="showAddTaskModal = true"
      class="lg:hidden fixed right-6 bottom-6 h-14 w-14 rounded-full bg-emerald-600 text-white shadow-lg flex items-center justify-center">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from 'vue';

// Page navigation
const currentPage = ref('dashboard');
const isSidebarOpen = ref(false);
const isProfileMenuOpen = ref(false);
const showAddTaskModal = ref(false);

// User data
const userName = ref('John Doe');
const userEmail = ref('john@example.com');
const userInitials = computed(() => {
  return userName.value
    .split(' ')
    .map(name => name[0])
    .join('')
    .toUpperCase();
});

// Dark mode
const isDarkMode = ref(false);
const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark');
  } else {
    document.documentElement.classList.remove('dark');
  }
  localStorage.setItem('darkMode', isDarkMode.value);
};

// Task state
const tasks = ref([]);
const newTask = ref({
  title: '',
  completed: false,
  category: 'work',
  priority: 'medium',
  dueDate: ''
});

// Editing state
const editingTask = ref(null);
const editedTitle = ref('');

// Filters
const searchQuery = ref('');
const filterStatus = ref('all');
const filterCategory = ref('all');
const filterPriority = ref('all');

// Page title based on current page
const pageTitle = computed(() => {
  const titles = {
    dashboard: 'Dashboard',
    tasks: 'Tasks',
    analytics: 'Analytics',
    settings: 'Settings'
  };
  return titles[currentPage.value] || 'TaskMaster';
});

// Change page
const changePage = (page) => {
  currentPage.value = page;
  isSidebarOpen.value = false;
  isProfileMenuOpen.value = false;
};

// Add a new task
const addTask = () => {
  if (newTask.value.title.trim() === '') return;

  tasks.value.push({
    id: Date.now(),
    title: newTask.value.title,
    completed: false,
    category: newTask.value.category,
    priority: newTask.value.priority,
    dueDate: newTask.value.dueDate,
    createdAt: new Date().toISOString(),
    completedAt: null
  });

  // Reset form
  newTask.value = {
    title: '',
    completed: false,
    category: 'work',
    priority: 'medium',
    dueDate: ''
  };

  // Save to local storage
  saveTasks();

  // Close modal if open
  showAddTaskModal.value = false;
};

// Toggle task completion
const toggleComplete = (task) => {
  task.completed = !task.completed;
  task.completedAt = task.completed ? new Date().toISOString() : null;
  saveTasks();
};

// Delete a task
const deleteTask = (task) => {
  const index = tasks.value.findIndex(t => t.id === task.id);
  if (index !== -1) {
    tasks.value.splice(index, 1);
    saveTasks();
  }
};

// Start editing a task
const startEdit = (task) => {
  editingTask.value = task;
  editedTitle.value = task.title;
};

// Save edited task
const saveEdit = () => {
  if (editedTitle.value.trim() !== '') {
    editingTask.value.title = editedTitle.value;
    saveTasks();
  }
  cancelEdit();
};

// Cancel editing
const cancelEdit = () => {
  editingTask.value = null;
  editedTitle.value = '';
};

// Clear all completed tasks
const clearCompleted = () => {
  tasks.value = tasks.value.filter(task => !task.completed);
  saveTasks();
};

// Format date for display
const formatDate = (dateString) => {
  if (!dateString) return '';
  const date = new Date(dateString);
  return date.toLocaleDateString();
};

// Check if task is overdue
const isOverdue = (task) => {
  if (!task.dueDate || task.completed) return false;
  const today = new Date();
  today.setHours(0, 0, 0, 0);
  const dueDate = new Date(task.dueDate);
  return dueDate < today;
};

// Export data as JSON
const exportData = () => {
  const dataStr = JSON.stringify(tasks.value);
  const dataUri = 'data:application/json;charset=utf-8,' + encodeURIComponent(dataStr);

  const exportFileDefaultName = 'taskmaster-data.json';

  const linkElement = document.createElement('a');
  linkElement.setAttribute('href', dataUri);
  linkElement.setAttribute('download', exportFileDefaultName);
  linkElement.click();
};

// Clear all data
const clearAllData = () => {
  if (confirm('Are you sure you want to delete all tasks? This action cannot be undone.')) {
    tasks.value = [];
    localStorage.removeItem('vue-todo-tasks');
  }
};

// Filtered tasks based on search and filters
const filteredTasks = computed(() => {
  return tasks.value.filter(task => {
    // Status filter
    if (filterStatus.value === 'active' && task.completed) return false;
    if (filterStatus.value === 'completed' && !task.completed) return false;

    // Category filter
    if (filterCategory.value !== 'all' && task.category !== filterCategory.value) return false;

    // Priority filter
    if (filterPriority.value !== 'all' && task.priority !== filterPriority.value) return false;

    // Search query
    if (searchQuery.value.trim() !== '') {
      const query = searchQuery.value.toLowerCase();
      return task.title.toLowerCase().includes(query);
    }

    return true;
  });
});

// Recent tasks for dashboard
const recentTasks = computed(() => {
  return [...tasks.value]
    .sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt))
    .slice(0, 5);
});

// Recently completed tasks
const recentlyCompletedTasks = computed(() => {
  return tasks.value
    .filter(task => task.completed && task.completedAt)
    .sort((a, b) => new Date(b.completedAt) - new Date(a.completedAt))
    .slice(0, 5);
});

// Upcoming tasks
const upcomingTasks = computed(() => {
  const today = new Date();
  today.setHours(0, 0, 0, 0);

  return tasks.value
    .filter(task => !task.completed && task.dueDate && new Date(task.dueDate) >= today)
    .sort((a, b) => new Date(a.dueDate) - new Date(b.dueDate))
    .slice(0, 5);
});

// Task counts
const completedTasksCount = computed(() => {
  return tasks.value.filter(task => task.completed).length;
});

const pendingTasksCount = computed(() => {
  return tasks.value.filter(task => !task.completed).length;
});

const overdueTasksCount = computed(() => {
  return tasks.value.filter(task => isOverdue(task)).length;
});

// Completion rate
const completionRate = computed(() => {
  if (tasks.value.length === 0) return 0;
  return (completedTasksCount.value / tasks.value.length) * 100;
});

// Tasks by category
const tasksByCategory = computed(() => {
  const categories = {};
  tasks.value.forEach(task => {
    if (!categories[task.category]) {
      categories[task.category] = 0;
    }
    categories[task.category]++;
  });
  return categories;
});

// Tasks by priority
const tasksByPriority = computed(() => {
  const priorities = {
    low: 0,
    medium: 0,
    high: 0
  };
  tasks.value.forEach(task => {
    priorities[task.priority]++;
  });
  return priorities;
});

// Save tasks to local storage
const saveTasks = () => {
  localStorage.setItem('vue-todo-tasks', JSON.stringify(tasks.value));
};

// Load tasks
const loadTasks = () => {
  const savedTasks = localStorage.getItem('vue-todo-tasks');
  if (savedTasks) {
    tasks.value = JSON.parse(savedTasks);
  } else {
    // Add sample tasks if no tasks exist
    tasks.value = [
      {
        id: 1,
        title: 'Complete project proposal',
        completed: false,
        category: 'work',
        priority: 'high',
        dueDate: new Date(Date.now() + 86400000 * 2).toISOString().split('T')[0],
        createdAt: new Date().toISOString(),
        completedAt: null
      },
      {
        id: 2,
        title: 'Buy groceries',
        completed: true,
        category: 'shopping',
        priority: 'medium',
        dueDate: new Date().toISOString().split('T')[0],
        createdAt: new Date(Date.now() - 86400000).toISOString(),
        completedAt: new Date().toISOString()
      },
      {
        id: 3,
        title: 'Schedule doctor appointment',
        completed: false,
        category: 'health',
        priority: 'medium',
        dueDate: new Date(Date.now() + 86400000 * 5).toISOString().split('T')[0],
        createdAt: new Date(Date.now() - 86400000 * 2).toISOString(),
        completedAt: null
      }
    ];
    saveTasks();
  }
};

// Check for dark mode preference
const loadDarkModePreference = () => {
  const darkMode = localStorage.getItem('darkMode');
  if (darkMode === 'true') {
    isDarkMode.value = true;
    document.documentElement.classList.add('dark');
  }
};

// Watch for changes to save
watch(tasks, () => {
  saveTasks();
}, { deep: true });

// Initialize app
onMounted(() => {
  loadTasks();
  loadDarkModePreference();
});
</script>

<style>
.animate-fadeIn {
  animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Add Tailwind dark mode support */
@media (prefers-color-scheme: dark) {
  .dark\:bg-gray-900 {
    background-color: rgb(17, 24, 39);
  }

  .dark\:bg-gray-800 {
    background-color: rgb(31, 41, 55);
  }

  .dark\:bg-gray-700 {
    background-color: rgb(55, 65, 81);
  }

  .dark\:text-white {
    color: rgb(255, 255, 255);
  }

  .dark\:text-gray-300 {
    color: rgb(209, 213, 219);
  }

  .dark\:text-gray-400 {
    color: rgb(156, 163, 175);
  }

  .dark\:border-gray-700 {
    border-color: rgb(55, 65, 81);
  }

  .dark\:border-gray-600 {
    border-color: rgb(75, 85, 99);
  }
}
</style>