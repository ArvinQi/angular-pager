/**
 * Created by Arvin on 2016/6/21.
 */
(function () {
    /**
     * Config
     */
    var moduleName = 'angular.pager';

    /**
     * Module
     */
    var module;
    try {
        module = angular.module(moduleName);
    } catch (err) {
        // named module does not exist, so create one
        module = angular.module(moduleName, []);
    }
    var log = function (object) {
        console.log(object);
    };
    module
        .directive('ngPager', [ngPager]);

    function ngPager() {
        return {
            restrict: 'AE',
            // scope: {
            //     maxSize: '=?',
            //     onPageChange: '&?',
            //     paginationId: '=?'
            // },
            link: pager
        };
        function pager(scope, element, attrs) {
            var pagerParentDom = element[0];
            var dataScope = pagerParentDom.getAttribute('pager-data');
            var dataTotal = pagerParentDom.getAttribute('pager-total');
            var dataFunc = pagerParentDom.getAttribute('pager-func');
            var pagerDom = document.createElement('ul');
            var click = false;
            // var pageCount = 1;
            pagerDom.classList.add('pagination');
            pagerDom.classList.add('col-xs-12');
            // scope.pager = {
            //     currentPage: 1,
            //     pageSize: 6,
            //     total: 1
            // };
            var initPager = function(pageCount){
                // pageCount = scope.$eval(dataTotal) / scope.pager.pageSize;

                var pageCount = Math.ceil(scope.$eval(dataTotal) / scope.pager.pageSize);
                if(!pageCount){return}
                scope.pager.total = pageCount;
                var pagerList = '';
                pagerList += '<li page="0" class="first"><a>First</a></li>';
                pagerList += '<li page="0" class="prev '+(scope.pager.currentPage == 1?'disabled':'')+'"><a>Prev</a></li>';
                // var pageBegin1 = pageBegin ? pageBegin : 1;
                // var pageEnd1 = pageEnd ? pageEnd : pageCount;
                var pageBegin = 1;
                var pageEnd = 1;
                var currentPage = parseInt(scope.pager.currentPage);
                if(pageCount <= 5){
                    pageEnd = pageCount;
                }else{
                    if(currentPage >= 3 && currentPage <= pageCount - 2){
                        pageBegin = currentPage - 2;
                        pageEnd = currentPage + 2;
                    }else if(currentPage > pageCount - 2){
                        pageBegin = pageCount - 4;
                        pageEnd = pageCount;
                    }else{
                        pageEnd = 5;
                    }
                }
                for (var i = pageBegin; i <= pageEnd; i++ ) {
                    pagerList += '<li class="'+ (i == currentPage? 'active':'') +'" page="' + i + '"><a>' + i + '</a></li>';
                }

                pagerList += '<li page="0" class="next '+(scope.pager.currentPage == scope.pager.total?'disabled':'')+'"><a>Next</a></li>';
                pagerList += '<li page="0" class="last"><a>Last</a></li>';
                pagerDom.innerHTML = '';
                pagerDom.innerHTML = pagerList;
                element.html(pagerDom);
                element.find('a').css('user-select', 'none');
            };
            // setTimeout(function(){
            //     initPager(Math.ceil(scope.$eval(dataTotal) / scope.pager.pageSize));
            // }, 1000);
            element.on('click', 'ul li', function (e) {
                e.preventDefault();
                // var PrevorNext = false;
                var clickDom = e.target.parentNode;
                var current = clickDom.getAttribute('page');
                // var prevDom = pagerParentDom.querySelector('.prev');
                // var nextDom = pagerParentDom.querySelector('.next');
                if (clickDom.className.contains('prev')) {
                    current = parseInt(scope.pager.currentPage) - 1;
                }
                if (clickDom.className.contains('next')) {
                    current = parseInt(scope.pager.currentPage) + 1;
                }
                if (clickDom.className.contains('first')) {
                    current = 1;
                }
                if (clickDom.className.contains('last')) {
                    current = scope.pager.total;
                }
                if(clickDom.className.contains('disabled')||click||current == scope.pager.currentPage){
                    return false;
                }
                click = true;
                scope.pager.currentPage = current;
                // if(PrevorNext){
                //     clickDom = document.querySelector('[page="'+ scope.pager.currentPage +'"]');
                //     // scope.pager.currentPage = scope.pager.currentPage;
                // }else{
                //     clickDom = document.querySelector('[page="'+ current +'"]');

                    // scope.pager.currentPage = current;
                    // clickDom
                    //     .classList
                    //     .add('active')
                    //     .parents('ul')
                    //     .find('.active')
                    //     .classList
                    //     .remove('active');
                // }
                // if(scope.pager.currentPage == 1){
                //     // prevDom.setAttribute('disabled', 'disabled');
                //     prevDom.classList.add('disabled');
                // }else{
                //     // prevDom.removeAttribute('disabled');
                //
                //     prevDom.classList.remove('disabled');
                // }
                // if(scope.pager.currentPage == scope.pager.total){
                //     // nextDom.setAttribute('disabled', 'disabled');
                //     nextDom.classList.add('disabled');
                // }else{
                //     // nextDom.removeAttribute('disabled');
                //     nextDom.classList.remove('disabled');
                // }
                // pagerParentDom
                //     .querySelector('.active')
                //     .classList
                //     .remove('active');
                // clickDom
                //     .classList
                //     .add('active');
                initPager();
                //get data
                scope.$eval(dataFunc)();
            });
            scope.$watch(dataScope, function (value) {
                click = false;
            }, true);
            scope.$watch(dataTotal, function (value) {
                if(value != null) {
                    initPager();
                }
            }, true);
            //reset currentPage func
            scope.resetCurrentPage = function () {
                scope.pager.currentPage = 1;
            };

        }
    }

})();
