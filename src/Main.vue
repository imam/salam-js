<template>
    <div class="wrapper">
        <nav id="sidebar" :class="['sidebar ' , sidebarCollapsed ? 'collapsed' : null]">
        <div class="sidebar-content js-simplebar">
            <inertia-link class="sidebar-brand" href="/menu">
            <span class="align-middle">SIAP</span>
            </inertia-link>

            <ul class="sidebar-nav">
            <li class="sidebar-header">
                User Management
            </li>

            <li :class="['sidebar-item', $route().current('users.*') ? 'active': null]" >
                <inertia-link class="sidebar-link" href="/users">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Users</span>
                </inertia-link>
            </li>
            <li :class="['sidebar-item', $route().current('families.*') ? 'active': null]" >
                <inertia-link class="sidebar-link" href="/families">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Families</span>
                </inertia-link>
            </li>

            <li class="sidebar-header" >
                Cluster Management
            </li>
            <li :class="['sidebar-item', $route().current('clusters.*') ? 'active': null]" >
                <inertia-link class="sidebar-link" href="/clusters">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Clusters</span>
                </inertia-link>
            </li>
            <li :class="['sidebar-item', $route().current('cluster_blocks.*') ? 'active': null]">
                <inertia-link class="sidebar-link" href="/cluster_blocks">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Cluster Blocks</span>
                </inertia-link>
            </li>
            <li :class="['sidebar-item', $route().current('cluster_units.*') ? 'active': null]" >
                <inertia-link class="sidebar-link" href="/cluster_units">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Cluster Units</span>
                </inertia-link>
            </li>

            <li class="sidebar-header">
                Admin Management
            </li>
            <li :class="['sidebar-item', $route().current('admins.*') ? 'active': null]">
                <inertia-link class="sidebar-link" href="/admins">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Admins</span>
                </inertia-link>
            </li>

            <li class="sidebar-header">Invoice Management</li>
            <li :class="['sidebar-item', $route().current('invoices.*') ? 'active': null]">
                <inertia-link class="sidebar-link" href="/invoices">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Invoices</span>
                </inertia-link>
            </li>
            <li :class="['sidebar-item', $route().current('receipts.*') ? 'active': null]">
                <inertia-link class="sidebar-link" href="/receipts">
                    <i class="align-middle" data-feather="sliders"></i> <span class="align-middle">Receipts</span>
                </inertia-link>
            </li>

            
            </ul>
        </div>
        </nav>

        <div class="main">
        <nav class="navbar navbar-expand navbar-light navbar-bg">
            <a class="sidebar-toggle d-flex" @click="toggleSidebar()">
            <i class="hamburger align-self-center"></i>
            </a>

            <div class="navbar-collapse collapse">
            <ul class="navbar-nav navbar-align" >
                <li :class="['nav-item dropdown', ]" v-click-outside="() => openProfileCard(false)">
                <a @click.prevent="openProfileCard(true)" class="nav-icon dropdown-toggle d-inline-block d-sm-none" href="#" data-toggle="dropdown">
                    <i class="align-middle" data-feather="settings"></i>
                </a>

                <a @click.prevent="openProfileCard(true)" class="nav-link dropdown-toggle d-none d-sm-inline-block" href="#" data-toggle="dropdown">
                    <span class="text-dark">{{$inertia.page.props.current_user? $inertia.page.props.current_user.user_full_name: null}}</span>
                </a>
                <div :class="['dropdown-menu dropdown-menu-right', isProfileCardOpen ? 'show': null]">
                    <a class="dropdown-item flex" href="/profile"><i class="align-middle mr-1" data-feather="user"></i> Profile</a>
                    <div class="dropdown-divider"></div>
                    <a class="dropdown-item" href="/logout">Log out</a>
                </div>
                </li>
            </ul>
            </div>
        </nav>

        <main class="content">
            <slot></slot>
        </main>

        <footer class="footer">
            <div class="container-fluid">
            <div class="row text-muted">
                <div class="col-6 text-left">
                <p class="mb-0">
                    <a href="/menu" class="text-muted"><strong>SIAP</strong></a> &copy; 
                </p>
                </div>
                <div class="col-6 text-right">
                </div>
            </div>
            </div>
        </footer>
        </div>
    </div>
</template>

<script>
    import vClickOutside from 'v-click-outside'

    export default {
        directives: {
            clickOutside: vClickOutside.directive
        },
        methods: {
            toggleSidebar() {
                this.sidebarCollapsed = !this.sidebarCollapsed
            },
            openProfileCard(open) {
                 this.isProfileCardOpen = open
            }
        },
        data() {
            return {
                sidebarCollapsed: false,
                isProfileCardOpen: false
            }
        },
        mounted() {
            this.$inertia.on('success', () => {
                if(this.$page.props.flash.success){
                    this.$fire({
                        type: 'success',
                        title: this.$page.props.flash.success
                    })
                }
            })
        },
    }
</script>
